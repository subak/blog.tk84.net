# Pandoc の Syntax highlighting のカラースキームを Solarized にする 

`Pandoc` が自動的に出力するcssはこんな感じ

```css
div.sourceCode { overflow-x: auto; }
table.sourceCode, tr.sourceCode, td.lineNumbers, td.sourceCode {
  margin: 0; padding: 0; vertical-align: baseline; border: none; }
table.sourceCode { width: 100%; line-height: 100%; }
td.lineNumbers { text-align: right; padding-right: 4px; padding-left: 4px; background-color: #dddddd; }
td.sourceCode { padding-left: 5px; }
code > span.kw { font-weight: bold; } /* Keyword */
code > span.dt { color: #800000; } /* DataType */
code > span.dv { color: #0000ff; } /* DecVal */
code > span.bn { color: #0000ff; } /* BaseN */
code > span.fl { color: #800080; } /* Float */
code > span.ch { color: #ff00ff; } /* Char */
code > span.st { color: #dd0000; } /* String */
code > span.co { color: #808080; font-style: italic; } /* Comment */
code > span.al { color: #00ff00; font-weight: bold; } /* Alert */
code > span.fu { color: #000080; } /* Function */
code > span.er { color: #ff0000; font-weight: bold; } /* Error */
code > span.wa { color: #ff0000; font-weight: bold; } /* Warning */
code > span.cn { color: #000000; } /* Constant */
code > span.sc { color: #ff00ff; } /* SpecialChar */
code > span.vs { color: #dd0000; } /* VerbatimString */
code > span.ss { color: #dd0000; } /* SpecialString */
code > span.im { } /* Import */
code > span.va { } /* Variable */
code > span.cf { } /* ControlFlow */
code > span.op { } /* Operator */
code > span.bu { } /* BuiltIn */
code > span.ex { } /* Extension */
code > span.pp { font-weight: bold; } /* Preprocessor */
code > span.at { } /* Attribute */
code > span.do { color: #808080; font-style: italic; } /* Documentation */
code > span.an { color: #808080; font-weight: bold; font-style: italic; } /* Annotation */
code > span.cv { color: #808080; font-weight: bold; font-style: italic; } /* CommentVar */
code > span.in { color: #808080; font-weight: bold; font-style: italic; } /* Information */
```

これを `Solarized` にします。

## Paygments を参考にする

`Pandoc` では `Syntax highlighting` に `highlighting-kate` を使っています。[^1]  
`Sorlized` のcssがどこかにあれば良いのですが見つからないので自分で書くことにしました。

とはいえできるだけ楽に済ませたいです。
`Paygments` のcssを見つけた[^2]のでこれを参考に `highlighting-kate` のcssを修正します。

cssはこんな感じ

```css
td.linenos { background-color: #f0f0f0; padding-right: 10px; }
span.lineno { background-color: #f0f0f0; padding: 0 5px 0 5px; }
pre { line-height: 125%; }
body .hll { background-color: #ffffcc }
body  { background: #ffffff; color: #93a1a1; background-color: #002b36 }
body .c { color: #586e75; background-color: #002b36 } /* Comment */
body .err { color: #93a1a1; background-color: #002b36 } /* Error */
body .g { color: #93a1a1; background-color: #002b36 } /* Generic */
body .k { color: #859900; background-color: #002b36 } /* Keyword */
body .l { color: #93a1a1; background-color: #002b36 } /* Literal */
body .n { color: #93a1a1; background-color: #002b36 } /* Name */
body .o { color: #93a1a1; background-color: #002b36 } /* Operator */
body .x { color: #93a1a1; background-color: #002b36 } /* Other */
body .p { color: #93a1a1; background-color: #002b36 } /* Punctuation */
body .cm { color: #586e75; background-color: #002b36 } /* Comment.Multiline */
body .cp { color: #586e75; background-color: #002b36 } /* Comment.Preproc */
body .c1 { color: #586e75; background-color: #002b36 } /* Comment.Single */
body .cs { color: #586e75; background-color: #002b36 } /* Comment.Special */
body .gd { color: #93a1a1; background-color: #002b36 } /* Generic.Deleted */
body .ge { color: #93a1a1; background-color: #002b36 } /* Generic.Emph */
body .gr { color: #93a1a1; background-color: #002b36 } /* Generic.Error */
body .gh { color: #93a1a1; background-color: #002b36 } /* Generic.Heading */
body .gi { color: #93a1a1; background-color: #002b36 } /* Generic.Inserted */
body .go { color: #93a1a1; background-color: #002b36 } /* Generic.Output */
body .gp { color: #93a1a1; background-color: #002b36 } /* Generic.Prompt */
body .gs { color: #93a1a1; background-color: #002b36 } /* Generic.Strong */
body .gu { color: #93a1a1; background-color: #002b36 } /* Generic.Subheading */
body .gt { color: #93a1a1; background-color: #002b36 } /* Generic.Traceback */
body .kc { color: #2aa198; background-color: #002b36 } /* Keyword.Constant */
body .kd { color: #268bd2; background-color: #002b36 } /* Keyword.Declaration */
body .kn { color: #cb4b16; background-color: #002b36 } /* Keyword.Namespace */
body .kp { color: #859900; background-color: #002b36 } /* Keyword.Pseudo */
body .kr { color: #859900; background-color: #002b36 } /* Keyword.Reserved */
body .kt { color: #859900; background-color: #002b36 } /* Keyword.Type */
body .ld { color: #93a1a1; background-color: #002b36 } /* Literal.Date */
body .m { color: #2aa198; background-color: #002b36 } /* Literal.Number */
body .s { color: #2aa198; background-color: #002b36 } /* Literal.String */
body .na { color: #93a1a1; background-color: #002b36 } /* Name.Attribute */
body .nb { color: #dc322f; background-color: #002b36 } /* Name.Builtin */
body .nc { color: #268bd2; background-color: #002b36 } /* Name.Class */
body .no { color: #93a1a1; background-color: #002b36 } /* Name.Constant */
body .nd { color: #268bd2; background-color: #002b36 } /* Name.Decorator */
body .ni { color: #6c71c4; background-color: #002b36 } /* Name.Entity */
body .ne { color: #b58900; background-color: #002b36 } /* Name.Exception */
body .nf { color: #268bd2; background-color: #002b36 } /* Name.Function */
body .nl { color: #93a1a1; background-color: #002b36 } /* Name.Label */
body .nn { color: #93a1a1; background-color: #002b36 } /* Name.Namespace */
body .nx { color: #93a1a1; background-color: #002b36 } /* Name.Other */
body .py { color: #93a1a1; background-color: #002b36 } /* Name.Property */
body .nt { color: #93a1a1; background-color: #002b36 } /* Name.Tag */
body .nv { color: #93a1a1; background-color: #002b36 } /* Name.Variable */
body .ow { color: #859900; background-color: #002b36 } /* Operator.Word */
body .w { color: #93a1a1; background-color: #002b36 } /* Text.Whitespace */
body .mf { color: #2aa198; background-color: #002b36 } /* Literal.Number.Float */
body .mh { color: #2aa198; background-color: #002b36 } /* Literal.Number.Hex */
body .mi { color: #2aa198; background-color: #002b36 } /* Literal.Number.Integer */
body .mo { color: #2aa198; background-color: #002b36 } /* Literal.Number.Oct */
body .sb { color: #2aa198; background-color: #002b36 } /* Literal.String.Backtick */
body .sc { color: #2aa198; background-color: #002b36 } /* Literal.String.Char */
body .sd { color: #2aa198; background-color: #002b36 } /* Literal.String.Doc */
body .s2 { color: #2aa198; background-color: #002b36 } /* Literal.String.Double */
body .se { color: #2aa198; background-color: #002b36 } /* Literal.String.Escape */
body .sh { color: #2aa198; background-color: #002b36 } /* Literal.String.Heredoc */
body .si { color: #2aa198; background-color: #002b36 } /* Literal.String.Interpol */
body .sx { color: #2aa198; background-color: #002b36 } /* Literal.String.Other */
body .sr { color: #2aa198; background-color: #002b36 } /* Literal.String.Regex */
body .s1 { color: #2aa198; background-color: #002b36 } /* Literal.String.Single */
body .ss { color: #2aa198; background-color: #002b36 } /* Literal.String.Symbol */
body .bp { color: #268bd2; background-color: #002b36 } /* Name.Builtin.Pseudo */
body .vc { color: #93a1a1; background-color: #002b36 } /* Name.Variable.Class */
body .vg { color: #93a1a1; background-color: #002b36 } /* Name.Variable.Global */
body .vi { color: #93a1a1; background-color: #002b36 } /* Name.Variable.Instance */
body .il { color: #2aa198; background-color: #002b36 } /* Literal.Number.Integer.Long */
```

## 解析

それぞれのCSSにはコメントで `Keyword`, `Comment` などのトークンタイプがありますのでこれを対応させてゆきます。  
`Paygments` の方がトークンタイプが多いのでそこは適当に。

## 成果

とりあえずこんな感じにしてみました。

```css
div.sourceCode { overflow-x: auto; }
table.sourceCode, tr.sourceCode, td.lineNumbers, td.sourceCode {
  margin: 0; padding: 0; vertical-align: baseline; border: none; }
table.sourceCode { width: 100%; line-height: 100%; }
td.lineNumbers { text-align: right; padding-right: 4px; padding-left: 4px; color: #aaaaaa; border-right: 1px solid #aaaaaa; }
pre.sourceCode { color: #93a1a1; background-color: #002b36; }
code > span.kw { color: #268bd2; } /* Keyword */
code > span.dt { color: #93a1a1; } /* DataType */
code > span.dv { color: #2aa198; } /* DecVal */
code > span.bn { color: #0000ff; } /* BaseN */
code > span.fl { color: #2aa198; } /* Float */
code > span.ch { color: #2aa198; } /* Char */
code > span.st { color: #2aa198; } /* String */
code > span.co { color: #586e75; } /* Comment */
/*code > span.al { color: #00ff00; font-weight: bold; }*/ /* Alert */
code > span.fu { color: #268bd2; } /* Function */
/*code > span.er { color: #ff0000; font-weight: bold; }*/ /* Error */
/*code > span.wa { color: #ff0000; font-weight: bold; }*/ /* Warning */
code > span.cn { color: #93a1a1; } /* Constant */
code > span.sc { color: #2aa198; } /* SpecialChar */
/*code > span.vs { color: #dd0000; }*/ /* VerbatimString */
/*code > span.ss { color: #dd0000; }*/ /* SpecialString */
code > span.im { } /* Import */
code > span.va { color: #93a1a1; } /* Variable */
code > span.cf { } /* ControlFlow */
code > span.op { color: #859900; } /* Operator */
code > span.bu { color: #dc322f; } /* BuiltIn */
code > span.ex { } /* Extension */
/*code > span.pp { font-weight: bold; }*/ /* Preprocessor */
code > span.at { color: #93a1a1; } /* Attribute */
/*code > span.do { color: #808080; font-style: italic; }*/ /* Documentation */
/*code > span.an { color: #808080; font-weight: bold; font-style: italic; }*/ /* Annotation */
/*code > span.cv { color: #808080; font-weight: bold; font-style: italic; }*/ /* CommentVar */
/*code > span.in { color: #808080; font-weight: bold; font-style: italic; }*/ /* Information */
```

対応がわからなかったのはとりあえずコメントアウトしてます。  
折を見て手直しします。


[^1]: デフォルト設定。オプションで他のカラースキーマを選択できます。http://pandoc.org/MANUAL.html#syntax-highlighting
[^2]: http://honza.ca/solarized-pygments/