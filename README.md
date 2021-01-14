# usefull-R-things

## Color Pallete

### see colors and numbers
```
library("RColorBrewer")
display.brewer.all()
```
### View a single RColorBrewer palette by specifying its name
```
display.brewer.pal(n = 8, name = 'RdBu')
```
### Hexadecimal color specification 
```
brewer.pal(n = 8, name = "RdBu")
```
### interactive 

link [here](https://www.nceas.ucsb.edu/sites/default/files/2020-04/colorPaletteCheatsheet.pdf)
```
library("colorspace")
pal <- choose_palette()
```

## Kable:
 to generate pretty tables, but only works in htmls. Does not really works when knitting to pdfs ( teh style gets messed up
```
pack_row <-  class_tbl %>% group_by(Phylum) %>% tally() %>% 
  mutate(end= cumsum(n),start = end-n+1) %>% 
  mutate(Phylum=as.character(Phylum))
  
  full_join(class_dt_meso,class_dt_macro, by=c("Phylum", 'Class')) %>% ungroup() %>% 
 # dplyr::select(-Phylum) %>% 
    mutate( across(everything(), ~replace_na(.x, "-"))) %>% 
  kbl(col.names = c("Phylum: Class","n","%","n","%"),
      caption = "Number of entries, n, (with percent, %) for 19 Phyla from the mesopelagic dataset groupped by organisms' class and net size (Meso and Macro)") %>% 
  kable_classic(full_width = FALSE) %>%
  add_header_above(c(" " = 1, "Meso" = 2, "Macro" = 2)) %>%
  pack_rows(pack_row$Phylum[1], pack_row$start[1], pack_row$end[1]) %>%
  pack_rows(pack_row$Phylum[2], pack_row$start[2], pack_row$end[2])%>%
```
