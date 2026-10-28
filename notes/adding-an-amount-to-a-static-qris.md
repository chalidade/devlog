# Adding an Amount to a Static QRIS

A shop's printed QRIS has no amount: the buyer scans it and types the price.
The [QRIS Nominal](https://chalidade.github.io/tools/) tool in tools takes that
static code and makes a new QR that already asks for, say, Rp25.000. It's all
string work in the browser, about 90 lines in
[`src/tools/qris/qris.ts`](https://github.com/chalidade/tools/blob/main/src/tools/qris/qris.ts).

## The format

QRIS is an EMV merchant-presented QR. The scanned text is a flat list of items,
each `tag (2 digits) + length (2 digits) + value`:

- starts with `000201` (tag 00, length 02, value `01`)
- tag `01` is `11` for static, `12` for dynamic
- tags 26–51 hold the merchant account data; tag `58` is the country (`ID`)
- tag `54` is the amount, `59` the merchant name, `60` the city
- the last item is tag `63`, a CRC-16 over everything before its four hex digits

## Making it ask for an amount

1. Parse the top level into items; reject it if it doesn't start with `000201`,
   if a length runs past the end, or if the country isn't `ID` or there's no
   merchant data
2. Drop any old `54` and the `63`, and set tag `01` to `12`
3. Insert tag `54` **in tag order** (before the first tag above 54), not at the
   end
4. Append `6304` and compute the CRC over the whole string including that
   `6304`

The CRC is CRC-16/CCITT-FALSE: polynomial `0x1021`, initial value `0xFFFF`,
over the UTF-8 bytes, written as four uppercase hex digits.

## Gotchas

- **Check the original CRC too.** If it doesn't match, the scan was misread or
  the code was altered. The tool still builds a correct new code but warns
- **The amount has no trailing zeros after the decimal point**: `25000` and
  `25000.5`, never `25000.50`. Input like `25.000` or `25.000,50` (Indonesian
  grouping) is normalised first
- Nothing leaves the device, and the tool says to use your own shop's QRIS
