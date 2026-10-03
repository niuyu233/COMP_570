# COMP_570
# Task 3: Explore My Little Pony Dataset Properties

## 1 How big is the dataset?

```shell
wc -l ./clean_dialog.csv
```

36860

## 2 What’s the structure of the data?

```shell
csvtool -t ',' col 1 ./clean_dialog.csv | head -5
```

title: episode title

```shell
csvtool -t ',' col 2 ./clean_dialog.csv | head -5
```

writer: writer of this episode

```shell
csvtool -t ',' col 3 ./clean_dialog.csv | head -5
```

pony: character who is speaking

```shell
csvtool -t ',' col 4 ./clean_dialog.csv | head -5
```

dialog: dialogue text

## 3 How many episodes does it cover?

```shell
csvtool -t ',' col 1 ./clean_dialog.csv | tail -n +2 | sort -u | wc -l
```

197

## 4 During the exploration phase, find at least one aspect of the dataset that is unexpected

```shell
csvtool -t ',' col 3 ../clean_dialog.csv | tail -n +2 | sort -u | grep "Twilight Sparkle"
```

When I searched the speakers column, I found different variations of Twilight Sparkle, such as Rainbow Dash and Twilight Sparkle. When searching for individual speakers, these entries may be counted twice, as if Rainbow Dash and Twilight Sparkle each spoke one line.



# Task 4: Analyze speaker frequency

```shell
TOTAL=$(($(wc -l < ../clean_dialog.csv)-1))
echo "pony_name,total_line_count,percent_all_lines" > Line_percentages.csv
for pony in "Twilight Sparkle" "Rarity" "Pinkie Pie" "Rainbow Dash" "Fluttershy"; do
    COUNT=$(csvtool -t ',' col 3 ../clean_dialog.csv | grep -c "^$pony$")
    PERCENT=$(echo "scale=2; $COUNT * 100 / $TOTAL" | bc)
    echo "$pony,$COUNT,$PERCENT%" >> Line_percentages.csv
done
```

saving the data to Line_percentages.csv
