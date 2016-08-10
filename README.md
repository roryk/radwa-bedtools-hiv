What you have to do to get this to work. I'm assuming the finished.BED file are
the Alu positions padded via `bedtools slop`.

1) fix the ^M line endings issue. You can do this by search and replacing ^M with a proper linefeed.
2) convert Maldarelli_IS.BED to a proper BED file (it needs at least three columns to be valid).

```bash
awk -v OFS='\t' '{print $0,$2}' Maldarelli_IS.BED > maldarelli.bed
```

3) count the number of times the features in `maldarelli.bed` overlap the features in `finished.BED`.

```bash
 bedtools intersect -c -a maldarelli.bed -b finished.BED
```

VERY IMPORTANT: make sure the alu regions are from the same genome build as the Maldarelli coordinates,
otherwise these results will be very very wrong.
