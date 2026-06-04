# Changing Jupyter Lab Syntax Colors


To change the syntax colors in JupyterLab installed via pip, you need to locate the default themes and the `index.css` file. These files are typically found in `~/.local/share/jupyter/lab/themes` if installed at the user level, or in `/usr/share/` if installed system-wide. The colors are defined in the `index.css` files, specifically within the block for CodeMirror styles, which includes variables like `--jp-mirror-editor-keyword-color` for keywords and `--jp-mirror-editor-string-color` for strings

For example, to change the color of the "import" keyword, you would modify the `--jp-mirror-editor-keyword-color` variable. You can find the specific path by running `jupyter --paths` and checking the directories under `data`

If you do not have these folders, it might be because JupyterLab installed via pip does not automatically create them. In such cases, you can manually create the necessary directories and files to customize the theme

---
## custom theme
the default themes rest @ `~/.local/share/jupyter/lab/themes` if installed at user level.  

[link](https://discourse.jupyter.org/t/how-can-i-change-code-colors-in-jupyter-lab-installed-via-pip/20147)

### my theme

`~/.local/share/jupyter/lab/themes/@jupyterlab/theme-dark-extension$`




  ```
/* Defaults use Material Design specification */
/* my custom colors */
/* --my-main-color:#D1B498; */
--my-main-color:#D6C8BC;
--jp-content-font-color0: var(--my-main-color);
--jp-content-font-color1: var(--my-main-color);
--jp-content-font-color2: var(--my-main-color);
--jp-content-font-color3: var(--my-main-color);
  
.
.
.

  /* Code mirror specific styles */
  /* my custom colors */
  /* bright purple color hex #AA22FF */
  --jp-mirror-editor-keyword-color: #C37D3B;
  --jp-mirror-editor-atom-color: #E7A0E9 ;
  --jp-mirror-editor-number-color: #89FFDC;
  --jp-mirror-editor-def-color: #C37D3B;
  --jp-mirror-editor-variable-color:#51D4FF;
  --jp-mirror-editor-variable-2-color:#51D4FF;
  --jp-mirror-editor-variable-3-color: #51D4FF;
  --jp-mirror-editor-punctuation-color:  #51D4FF;
  --jp-mirror-editor-property-color:#EBA22C;
  --jp-mirror-editor-operator-color: #C0A57A;
  --jp-mirror-editor-comment-color: #584E4C;
  --jp-mirror-editor-string-color: #DCADF0;
  --jp-mirror-editor-string-2-color:#B656DF;
  --jp-mirror-editor-meta-color: #a2f;
  --jp-mirror-editor-qualifier-color: #AA22FF;
  --jp-mirror-editor-builtin-color: #83D0E9;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: var(--md-green-700, #388e3c);
  --jp-mirror-editor-attribute-color:#AA22FF;
  --jp-mirror-editor-header-color:#AA22FF;
  --jp-mirror-editor-quote-color: #AA22FF;
  --jp-mirror-editor-link-color:#AA22FF;
  --jp-mirror-editor-error-color:#AA22FF;
  --jp-mirror-editor-hr-color: #AA22FF;
```
