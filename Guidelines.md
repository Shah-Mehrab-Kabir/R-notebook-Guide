# **R Notebook: Ultimate Cheat Sheet 🚀**

## **🎯 ESSENTIAL SHORTCUTS**

### **Document Navigation**
| Action | Windows/Linux | Mac |
|--------|--------------|-----|
| **New R Notebook** | Ctrl+Shift+N | Cmd+Shift+N |
| **Save** | Ctrl+S | Cmd+S |
| **Save All** | Ctrl+Alt+S | Cmd+Option+S |
| **Find** | Ctrl+F | Cmd+F |
| **Replace** | Ctrl+H | Cmd+H |
| **Find in Files** | Ctrl+Shift+F | Cmd+Shift+F |

### **Code Chunk Management**
| Action | Shortcut |
|--------|----------|
| **Insert Chunk** | Ctrl+Alt+I | Cmd+Option+I |
| **Run Current Chunk** | Ctrl+Shift+Enter | Cmd+Shift+Enter |
| **Run Next Chunk** | Alt+Ctrl+N | Option+Cmd+N |
| **Run All Chunks Above** | Ctrl+Alt+P | Cmd+Option+P |
| **Run All Chunks** | Ctrl+Alt+R | Cmd+Option+R |
| **Go to Next Chunk** | Alt+Ctrl+N | Option+Cmd+N |
| **Go to Previous Chunk** | Alt+Ctrl+P | Option+Cmd+P |

### **Editing & Formatting**
| Action | Shortcut |
|--------|----------|
| **Toggle Visual/Source** | Ctrl+Shift+F4 | Cmd+Shift+F4 |
| **Insert Pipe %>%** | Ctrl+Shift+M | Cmd+Shift+M |
| **Insert Assignment <-** | Alt+- | Option+- |
| **Comment/Uncomment** | Ctrl+Shift+C | Cmd+Shift+C |
| **Reformat Code** | Ctrl+Shift+A | Cmd+Shift+A |
| **Fold/Unfold Code** | Alt+L / Shift+Alt+L | Option+L / Shift+Option+L |

### **Knit & Preview**
| Action | Shortcut |
|--------|----------|
| **Knit Document** | Ctrl+Shift+K | Cmd+Shift+K |
| **Preview HTML** | Ctrl+Shift+H | Cmd+Shift+H |
| **Knit with Parameters** | Ctrl+Shift+Alt+K | Cmd+Shift+Option+K |

## **✨ POWER USER TRICKS**

### **1. Supercharged YAML Headers**
```yaml
---
title: "Smart Notebook"
output: 
  html_notebook:
    toc: true                    # Table of contents
    toc_float: true             # Floating TOC
    code_folding: hide          # Hide code initially
    theme: cerulean             # Bootstrap theme
    highlight: tango            # Syntax highlighting
params:
  data_file: "default.csv"      # Parameterized reports
  show_plots: true
date: "`r format(Sys.Date(), '%B %d, %Y')`"  # Auto-date
---
```

### **2. Magic Chunk Options**
```r
```{r, cache=TRUE, cache.path="cache/"}  # Cache for speed
# Slow computation here
```

```{r, fig.asp=0.618}  # Golden ratio plots
ggplot(...)
```

```{r, out.width="70%", fig.align='center'}  # Image sizing
plot(...)
```
```

### **3. Interactive Elements**
```r
# Interactive tables
DT::datatable(mtcars, 
              filter = 'top',
              options = list(pageLength = 5))

# Interactive plots
plotly::ggplotly(ggplot(mtcars, aes(mpg, wt)) + geom_point())

# Parameterized reports
# Use params$variable_name in code
```

### **4. Smart Caching Strategies**
```r
```{r load-data, cache=TRUE, cache.path="cache/"}
# Caches separately for different inputs
```

```{r compute, cache=TRUE, cache.extra=list(x, y)}
# Cache depends on variables x and y
```

# Clear cache when needed
knitr::clean_cache()
```

## **🚀 PRODUCTIVITY HACKS**

### **Template Chunks (Save as Snippets)**
1. **Tools → Global Options → Code → Edit Snippets**
2. Add custom snippets:
```
snippet myplot
    ```{r, fig.width=10, fig.height=6}
    ggplot(${1:data}, aes(${2:x}, ${3:y})) +
        geom_point() +
        theme_minimal()
    ```
```
3. Type `myplot` + Tab to insert

### **Keyboard Maestro (Advanced)**
```r
# Create custom shortcuts via Addins → Browse Addins → Keyboard Shortcuts
# Examples: 
# - Insert specific chunk template
# - Run and move to next chunk
# - Clear all output
```

### **Quick Navigation**
```r
# Bookmark lines: Shift+F2 (next), F2 (previous)
# Jump to function: Ctrl+. (period)
# Show outline: Ctrl+Shift+O
```

## **🔧 DEBUGGING & TROUBLESHOOTING**

### **Debug Mode**
```r
```{r, error=TRUE, warning=TRUE, message=TRUE}
# Shows all output including errors
```

# Debug specific chunk
options(error = browser)  # Enter browser() on error
```

### **Isolate Problem Areas**
```r
# Run in console to test chunk code
knitr::knit_code$get("chunk-name")

# Purge bad cache
unlink("*.Rmd_cache", recursive = TRUE)
```

### **Performance Monitoring**
```r
```{r, cache=TRUE, cache.lazy=FALSE}
# Force eager caching for large objects
```

# Time chunks
system.time({ your_code_here })
```

## **📁 PROJECT ORGANIZATION**

### **File Structure**
```
project/
├── analysis.Rmd              # Main notebook
├── notebooks/
│   ├── 01-explore.Rmd
│   ├── 02-model.Rmd
│   └── 03-visualize.Rmd
├── R/
│   ├── functions.R
│   └── helpers.R
├── data/
├── figs/                     # Auto-save figures
└── cache/                    # Chunk cache
```

### **Chunk Naming Convention**
```r
```{r 01_load-data}     # Prefix with order
```{r clean-variables}  # Descriptive
```{r fig-01-scatter}   # Figure naming
```
```

## **⚡ PERFORMANCE OPTIMIZATIONS**

### **1. Speed Up Knitting**
```r
# In setup chunk:
knitr::opts_chunk$set(
  cache = TRUE,
  autodep = TRUE,           # Auto dependency detection
  cache.lazy = FALSE        # Eager caching for large objects
)

# Use progress bars
pbapply::pblapply(data, function)
```

### **2. Memory Management**
```r
# Clear unused objects between sections
```{r, cache=FALSE}
rm(list = setdiff(ls(), "essential_data"))
gc()  # Garbage collection
```

### **3. Parallel Processing**
```r
```{r, cache=TRUE}
library(future)
plan(multisession)  # Parallel backend

# Use furrr for parallel dplyr
results <- future_map(data, analysis_function)
```
```

## **🔗 INTEGRATION TRICKS**

### **With Shiny**
```r
```{r, context="server"}
# Shiny server code
output$plot <- renderPlot({ ... })
```

runtime: shiny  # In YAML header
```

### **Python/R Mix**
```r
```{python}
import pandas as pd
df = pd.read_csv("data.csv")
```

```{r}
reticulate::py$df  # Access Python objects in R
```
```

### **SQL Integration**
```r
```{sql, connection=con, output.var="result"}
SELECT * FROM table LIMIT 10;
```

```{r}
# Use result in R
head(result)
```
```

## **🎨 VISUAL ENHANCEMENTS**

### **Custom CSS**
```css
<style>
.custom-box {
  padding: 10px;
  border: 2px solid #3498db;
  border-radius: 5px;
  background: #f8f9fa;
}
</style>

<div class="custom-box">
**Important Note:** This is a custom styled box.
</div>
```

### **HTML Widgets**
```r
# Animated progress
progress <- function(n) {
  cat("Progress: [", rep("=", n), ">", rep(" ", 10-n), "]\r", sep="")
}

# Colorful messages
crayon::blue("Processing...")
crayon::green("✓ Complete!")
```

## **📤 EXPORT & SHARING**

### **Multiple Outputs**
```r
# Knit to multiple formats
rmarkdown::render("notebook.Rmd", 
                  output_format = c("html_document", 
                                   "pdf_document",
                                   "word_document"))

# Create slides
rmarkdown::render("notebook.Rmd", "beamer_presentation")
```

### **Share Online**
```r
# Publish to RPubs
rsconnect::rpubsUpload(title = "My Analysis",
                       htmlFile = "notebook.html")

# Or RStudio Connect
rsconnect::deployDoc("notebook.Rmd")
```

## **🎯 QUICK REFERENCE CARDS**

### **Daily Use Card**
```
FREQUENT ACTIONS:
• New Chunk: Ctrl+Alt+I
• Run Chunk: Ctrl+Shift+Enter  
• Run All: Ctrl+Alt+R
• Knit: Ctrl+Shift+K
• Find Chunk: Ctrl+Shift+.
• Toggle Output: Ctrl+Shift+O
```

### **Chunk Options Cheat**
```
COMMON OPTIONS:
• echo=FALSE        # Hide code
• eval=FALSE        # Don't run  
• include=FALSE     # Run but hide all
• fig.width=7       # Plot width
• cache=TRUE        # Cache results
• warning=FALSE     # Suppress warnings
• message=FALSE     # Suppress messages
```

### **Troubleshooting Quick Fixes**
```
1. Clear chunk output: Run → Clear All Output
2. Reset cache: Delete *_cache folder
3. Update packages: install.packages("rmarkdown")
4. Check YAML: Must start/end with ---
5. Reset R session: Ctrl+Shift+F10
```

## **💡 PRO TIPS**

1. **Use `.Renviron` for secrets**: Never hardcode API keys
2. **Version control**: Git ignore `*_cache/` and `*.nb.html`
3. **Keyboard only workflow**: Learn 10 essential shortcuts
4. **Chunk references**: Use `ref.label` to reuse chunks
5. **Auto-completion**: `Ctrl+Space` for functions, `Tab` for arguments
6. **Quick view**: `Ctrl+Alt+V` for variable explorer
7. **Session info**: Include `sessionInfo()` at end
8. **Package loading**: Use `pacman::p_load()` for cleaner code

## **🔄 WORKFLOW AUTOMATION**

```r
# Auto-knit on save
options(rstudio.markdownToHTML = 
  function(inputFile, outputFile) {
    rmarkdown::render(inputFile, 
                      output_format = "html_document",
                      output_file = outputFile)
  })

# Batch process multiple notebooks
lapply(list.files(pattern = "*.Rmd"), rmarkdown::render)
```

---

**Save this as `RNotebook_Cheatsheet.Rmd` in your project!** 🎉

**Most Important:** Master these 5 shortcuts first:
1. `Ctrl+Alt+I` - Insert chunk
2. `Ctrl+Shift+Enter` - Run chunk  
3. `Ctrl+Alt+R` - Run all
4. `Ctrl+Shift+K` - Knit document
5. `Ctrl+Shift+F4` - Toggle view mode
