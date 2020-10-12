# Stain3_Standard_BR00115134

This a set of images from a 384-well plate. 

- 90 compounds  profiled in 4 replicates using the Cell Painting assay.
- The compound names have been anonymized.
- The file `load_data.csv` describes the mapping of images to channels and wells
- The file `platemap.csv` describs the mapping of wells to compounds (identified by the column `pert_id_index`)

Here's an overview of the data

```r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(magrittr))

load_data <- 
  read_csv("load_data.csv", col_types = cols(.default = "c")) %>%
  select(matches("FileName_|Metadata_Plate|Metadata_Well|Metadata_Site"))

platemap <- read_csv("platemap.csv", col_types = cols(.default = "c"))

load_data %>% 
  inner_join(platemap) %>%
  slice(1) %>%
  pivot_longer(everything()) %>%
  knitr::kable()
```

("description" added by hand)

|name                     |value                          |description|
|:------------------------|:------------------------------|-----------|
|Metadata_Plate           |BR00115134                     | Identifier of the 384-well plate | 
|Metadata_Well            |A01                            | Well identifier (e.g. `A01` refers to the top left well) | 
|Metadata_Site            |1                              | Site identifier. 9 sites were imaged per well in this dataset |
|Metadata_pert_id_index   |69                             | Compound identifier. The actual identity of the compound is hidden |
|FileName_OrigRNA         |r01c01f01p01-ch3sk1fk1fl1.tiff | Image of the RNA channel |
|FileName_OrigER          |r01c01f01p01-ch4sk1fk1fl1.tiff | Image of the ER channel |
|FileName_OrigAGP         |r01c01f01p01-ch2sk1fk1fl1.tiff | Image of the AGP channel |
|FileName_OrigMito        |r01c01f01p01-ch1sk1fk1fl1.tiff | Image of the Mito channel |
|FileName_OrigDNA         |r01c01f01p01-ch5sk1fk1fl1.tiff | Image of the DNA channel |
|FileName_OrigBrightfield |r01c01f01p01-ch6sk1fk1fl1.tiff | Image of the Brightfield channel |
