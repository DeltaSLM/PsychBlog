```{=org}
#+property: header-args:elisp :exports code
```
```{=org}
#+startup: fold
```
# Intro

One day I was bored, and in bordom i was redditing, and in redditing i
saw emacs, and then i wanted emacs, so voilas

I shoud definitely also mention that lots of this is plagerised...
mostly from some random 3000+line config I found on my PC which i have
no idea where from

# Doom Configuration

## Modules

Doom uses a *modular* configuration... thingy that makes emacs easier to
config.

``` {#init.el .commonlisp org-language="emacs-lisp" tangle="\"init.el\"" noweb="no-export" comments="no"}
;;; init.el -*- lexical-binding: t; -*-

;; This file controls what modules Doom loads and what order it does so in.
;; Press 'K' on a module to view documentation
;; use 'gd' to view a modules directory

(doom! :completion
       <<doom-completion>>

       :ui
       <<doom-ui>>

       :editor
       <<doom-editor>>

       :emacs
       <<doom-emacs>>

       :term
       <<doom-term>>

       :checkers
       <<doom-checkers>>

       :tools
       <<doom-tools>>

       :os
       <<doom-os>>

       :lang
       <<doom-lang>>

       :config
       <<doom-config>>

)
```

### Structure

This file is a literate configuration. We can do some things to make
this easier on us and doom, through the `literate` module

``` {#doom-config .commonlisp org-language="emacs-lisp" tangle="no"}
literate
(default +bindings +smartparens)
```

### Interface

We can enable lots of modules for this. Here we go!

``` {#doom-completion .commonlisp org-language="emacs-lisp" tangle="no"}
(company +childframe)           ; Code completion backend
(vertico +icons)                ; Search engine of the future
```

``` {#doom-ui .commonlisp org-language="emacs-lisp" tangle="no"}
doom                            ; What makes doom look how it does
doom-dashboard                  ; The splash screen we see upon emacs launch
doom-quit                       ; The cute little messages we see when we try to leave
(emoji +unicode)                ; 🙂
hl-todo                         ; highlighting TODO/FIXME/NOTE/DEPRECATED/HACK/REVIEW
(ligatures +extra)              ; ligatures and symbols to make code look good
minimap                         ; Show a map of the code at the side
modeline                        ; The snazzy thing at the bottom of our screen
nav-flash                       ; Blink the current line after switching
ophints                         ; Highlight the region an operation acts on
(popup +all +defaults)          ; Temporary Windows
treemacs                        ; Project tree/file switcher
vc-gutter                       ; vcs diff in the dringe
workspaces                      ; tab emulation/workspaces etc
zen                             ; distraction-free coding etc
```

``` {#doom-editor .commonlisp org-language="emacs-lisp" tangle="no"}
(evil +everywhere)              ; come to the dark side, we have cookies
file-templates                  ; auto-snippets for empty files
fold                            ; (nigh) universal code folding
(format)                        ; automated prettiness
snippets                        ; my elves. They type so I don't have to
```

``` {#doom-emacs .commonlisp org-language="emacs-lisp" tangle="no"}
(dired +icons)                  ; Make dired pretty again
electric                        ; smarter indenting
(ibuffer +icons)                ; buffer switching
undo                            ; better undo functionality
vc                              ; version-control
```

``` {#doom-term .commonlisp org-language="emacs-lisp" tangle="no"}
eshell                          ; the elisp shell that works everywhere
vterm                           ; the best terminal emulation in Emacs
```

``` {#doom-checkers .commonlisp org-language="emacs-lisp" tangle="no"}
syntax                          ; tasing you for every semicolon you forget
(:if (executable-find "aspell") spell) ; tasing you for misspelling mispelling
grammar                         ; tasing grammar mistake every you make
```

``` {#doom-tools .commonlisp org-language="emacs-lisp" tangle="no"}
(eval +overlay)                 ; run code, run (also, repls)
gist                            ; interacting with github gists
(lookup                         ; helps you navigate your code and documentation
 +dictionary                    ; dictionary/thesaurus is nice
 +docsets)                      ; ...or in Dash docsets locally
lsp                             ; Language Server Protocol
(magit                          ; a git porcelain for Emacs
 +forge)                        ; interface with git forges
make                            ; run make tasks from Emacs
pdf                             ; some weird format noone even uses i mean wtf
rgb                             ; creating color strings
```

``` {#doom-os .commonlisp org-language="emacs-lisp" tangle="no"}
(:if IS-MAC macos)              ; idec i dont use macos
tty                             ; improve the terminal Emacs experience
```

### Language Support

``` {#doom-lang .commonlisp org-language="emacs-lisp" tangle="no"}
cc                              ; C/C++/Obj-C madness
csharp                          ; unity, .NET, and mono shenanigans
emacs-lisp                      ; drown in parentheses
(javascript +lsp)               ; all(hope(abandon(ye(who(enter(here))))))
;;(latex                          ; writing papers in Emacs has never been so fun
;; +cdlatex                       ; quick maths symbols
;; +lsp
;; +fold)                         ; fold the clutter away nicities
json                            ; At least it ain't XML
(org                            ; organize your plain life in plain text
 +pretty                        ; yessss my pretties! (nice unicode symbols)
 +dragndrop                     ; drag & drop files/images into org buffers
 +jupyter                       ; ipython/jupyter support for babel
 +pandoc                        ; export-with-pandoc support
 +gnuplot                       ; who doesn't like pretty pictures
 +pomodoro                      ; be fruitful with the tomato technique
 +present                       ; using org-mode for presentations
 +roam2)                        ; wander around notes
(python +lsp +pyright)          ; beautiful is better than ugly
yaml                            ; JSON, but readable
```

## Packages

``` {#packages.el .commonlisp org-language="emacs-lisp" tangle="\"packages.el\"" noweb="no-export" comments="no"}
;; -*- no-byte-compile: t; -*-
;;; $DOOMDIR/packages.el

;; org
<<org>>

;; LaTeX
<<latex>>

;; Web
<<web>>

;; looks
<<looks>>

;; Tweaks
<<tweaks>>

;; Fun
<<fun>>
```

### Org

I spend lots of time in org-mode. Therefore, this needs to be good.

``` {#org .commonlisp org-language="emacs-lisp" tangle="no"}
(package! org-appear)
(package! org-super-agenda)
(package! doct :recipe (:host github :repo "progfolio/doct"))
(package! org-padding :recipe (:host github :repo "TonCherAmi/org-padding" ))
(package! org-ol-tree :recipe (:host github :repo "Townk/org-ol-tree"))
(package! org-pretty-table :recipe (:host github :repo "Fuco1/org-pretty-table"))
(package! org-roam-ui :recipe (:host github :repo "org-roam/org-roam-ui" :files ("*.el" "out")))
(package! org-pandoc-import
  :recipe (:host github
           :repo "tecosaur/org-pandoc-import"
           :files ("*.el" "filters" "preprocessors")))
```

### LaTeX

LaTex is an extremely useful tool for document-erising Lets add some
useful packages for that, too!

``` {#latex .commonlisp org-language="emacs-lisp" tangle="no"}
(package! org-fragtog)
(package! aas :recipe (:host github :repo "ymarco/auto-activating-snippets"))
(package! laas :recipe (:host github :repo "tecosaur/LaTeX-auto-activating-snippets"))
(package! engrave-faces :recipe (:host github :repo "tecosaur/engrave-faces"))
```

### Web

Some packages to help with... web? [ughh]{.ul}

``` {#web .commonlisp org-language="emacs-lisp" tangle="no"}
(package! ox-gfm)
(package! websocket)
```

1.  TODO

    -   Add <https://github.com/akirakyle/emacs-webkit> when it can be
        bothered to work

### Looks

Making emacs look good is most important, who even cares about
useability?

``` {#looks .commonlisp org-language="emacs-lisp" tangle="no"}
(unpin! doom-themes)
(unpin! doom-modeline)
(package! ox-chameleon :recipe (:host github :repo "tecosaur/ox-chameleon"))
```

### Tweaks

Some useful stuff to have in emacs

``` {#tweaks .commonlisp org-language="emacs-lisp" tangle="no"}
(package! screenshot :recipe (:host github :repo "tecosaur/screenshot"))
(package! lexic :recipe (:host github :repo "tecosaur/lexic"))
(package! swiper)
(package! vlf)
```

### Fun

Fun stuff to.. idk its just fun okay do i *really* need to explain
myself?

``` {#fun .commonlisp org-language="emacs-lisp" tangle="no"}
(package! xkcd)
(package! keycast)
```

# Basic Configuration

Make this config run just a litte bit faster... every little counts
(lexical bindings)

``` commonlisp
;;; config.el -*- lexical-binding: t; -*-
```

And make proper emacs optimisations

``` commonlisp
(when 'native-comp-compiler-options
                 (setq native-comp-compiler-options '("-O3" "-march=native" "-mtune=native")))
```

## Personal Info

``` commonlisp
(setq user-full-name "Teo Luppi"
      user-mail-address "teol@btinternet.com")
```

## Shell

Teling emacs to use my shell of choice: zsh

``` commonlisp
(setq explicit-shell-file-name (executable-find "zsh"))
```

## Vterm

And my emacs terminal emulator: VTERM!

Fix a bug with native-comp

``` commonlisp
(setq vterm-always-compile-module t)
```

Kill the buffer if the process exists

``` commonlisp
(setq vterm-kill-buffer-on-exit t)
```

Functions to get shell-side intergration going properly (+ a lil bit of
magit)

``` commonlisp
(after! vterm
  (setf (alist-get "magit-status" vterm-eval-cmds nil nil #'equal)
        '((lambda (path)
            (magit-status path)))))
```

Make ligatures work nicely

``` commonlisp
(setq +ligatures-in-modes t)
```

## Fonts

Strap in... font nerd means big font section :)

I like Iosevka a my main programming font (patched by nerd-fonts). I\'ll
also go with Overpass for my plain text font. I also prefer lighter
fonts, so i\'ll set that

``` commonlisp
;; --- Fonts
(setq doom-font (font-spec :family "Iosevka Nerd Font" :size 14)
      doom-big-font (font-spec :family "Iosevka Nerd Font" :size 20)
      doom-variable-pitch-font (font-spec :family "Overpass" :size 16)
      doom-unicode-font (font-spec :family "Iosevka Nerd Font")
      doom-serif-font (font-spec :family "Iosevka Nerd Font" :weight 'light))
```

For mixed pitched fonts, I\'m going to go with Alegraya, as it is fairly
comfy and generally nice

``` commonlisp
;; mixed pitch modes
(defvar mixed-pitch-modes '(org-mode LaTeX-mode markdown-mode gfm-mode Info-mode)) ;; Modes that mixed pitch mode should be enabled in
(defun init-mixed-pitch-h ()
  (when (memq major-mode mixed-pitch-modes)
    (mixed-pitch-mode 1))
  (dolist (hook mixed-pitch-modes)
    (add-hook (intern (concat (symbol-name hook) "-hook")) #'mixed-pitch-mode)))
(add-hook 'doom-init-ui-hook #'init-mixed-pitch-h)
(add-hook! 'org-mode-hook #'+org-pretty-mode)

;; Set mixed pitch font
(after! mixed-pitch
  (defface variable-pitch-serif
    '((t (:family "serif")))
    "A variable-pitch face with serifs."
    :group 'basic-faces)
  (setq mixed-pitch-set-height t)
  (setq variable-pitch-serif-font (font-spec :family "Alegreya" :size 16))
  (set-face-attribute 'variable-pitch-serif nil :font variable-pitch-serif-font)
  (defun mixed-pitch-serif-mode (&optional arg)
    (interactive)
    (let ((mixed-pitch-face 'variable-pitch-serif))
      (mixed-pitch-mode (or arg 'toggle)))))
```

Some nice harfbuzz ligatures

``` commonlisp
(set-char-table-range composition-function-table ?f '(["\\(?:ff?[fijlt]\\)" 0 font-shape-gstring]))
(set-char-table-range composition-function-table ?T '(["\\(?:Th\\)" 0 font-shape-gstring]))
```

Just in case the fonts aren\'t there, lets add check to notify the user
of the issue.

``` {#detect-missing-fonts .commonlisp org-language="emacs-lisp" tangle="no"}
(defvar required-fonts '("Overpass" "Alegreya" )) ;; Iosevka doesn't work properly but i need that for my terminal to launch so i dont think ill forget it
(defvar available-fonts
  (delete-dups (or (font-family-list)
                   (split-string (shell-command-to-string "fc-list : family")
                                 "[,\n]"))))
(defvar missing-fonts
  (delq nil (mapcar
             (lambda (font)
               (unless (delq nil (mapcar (lambda (f)
                           (string-match-p (format "^%s$" font) f))
                                         available-fonts))
                                         font))
                                         required-fonts)))
(if missing-fonts
    (pp-to-string
     `(unless noninteractive
        (add-hook! 'doom-init-ui-hook
          (run-at-time nil nil
                       (lambda ()
                         (message "%s missing the following fonts: %s"
                                  (propertize "Warning!" 'face '(bold warning))
                                  (mapconcat (lambda (font)
                                               (propertize font 'face 'font-lock-variable-name-face))
                                             ',missing-fonts
                                             ", "))
                         (sleep-for 0.5))))))
  ";; No missing fonts detected")
```

``` commonlisp
<<detect-missing-fonts()>>
```

## Themes

I\'m using one-dark for now, until tokyonight gets merged into
doom-themes. bit annoying but dealable with

``` commonlisp
(setq doom-theme 'doom-one)
(setq doom-themes-padded-modeline t)
```

## Large files

Making sure large files dont remove the living shit out of emacs (it
gets very laggy)

``` commonlisp
(require 'vlf-setup)
```

Now we can use `M-x vlf` to see a larger file in little batches.

## Company

Slow down company from suggesting everything, as it can be quite fast

``` commonlisp
(after! company
   (setq company-idle-delay 0.1
      company-minimum-prefix-length 1
      company-selection-wrap-around t
      company-require-match 'never
      company-dabbrev-downcase nil
      company-dabbrev-ignore-case t
      company-dabbrev-other-buffers nil
      company-tooltip-limit 5
      company-tooltip-minimum-width 50))
(set-company-backend!
  '(text-mode
    markdown-mode
    gfm-mode)
  '(:seperate
    company-yasnippet
    company-ispell
    company-files))

;;nested snippets
(setq yas-triggers-in-field t)
```

LaTeX Snippets

``` commonlisp
(use-package! aas
  :commands aas-mode)

(use-package! laas
  :hook (LaTeX-mode . laas-mode)
  :config
  (defun laas-tex-fold-maybe ()
    (unless (equal "/" aas-transient-snippet-key)
      (+latex-fold-last-macro-a)))
  (add-hook 'org-mode #'laas-mode)
  (add-hook 'aas-post-snippet-expand-hook #'laas-tex-fold-maybe))

```

Add those snippets while in org-mode (credit to henrik)

``` commonlisp
(defadvice! fixed-org-yas-expand-maybe-h ()
  "Expand a yasnippet snippet, if trigger exists at point or region is active.
Made for `org-tab-first-hook'."
  :override #'+org-yas-expand-maybe-h
  (when (and (featurep! :editor snippets)
             (require 'yasnippet nil t)
             (bound-and-true-p yas-minor-mode))
    (and (let ((major-mode (cond ((org-in-src-block-p t)
                                  (org-src-get-lang-mode (org-eldoc-get-src-lang)))
                                 ((org-inside-LaTeX-fragment-p)
                                  'latex-mode)
                                 (major-mode)))
               (org-src-tab-acts-natively nil) ; causes breakages
               ;; Smart indentation doesn't work with yasnippet, and painfully slow
               ;; in the few cases where it does.
               (yas-indent-line 'fixed))
           (cond ((and (or (not (bound-and-true-p evil-local-mode))
                           (evil-insert-state-p)
                           (evil-emacs-state-p))
                       (or (and (bound-and-true-p yas--tables)
                                (gethash major-mode yas--tables))
                           (progn (yas-reload-all) t))
                       (yas--templates-for-key-at-point))
                  (yas-expand)
                  t)
                 ((use-region-p)
                  (yas-insert-snippet)
                  t)))
         ;; HACK Yasnippet breaks org-superstar-mode because yasnippets is
         ;;      overzealous about cleaning up overlays.
         (when (bound-and-true-p org-superstar-mode)
           (org-superstar-restart)))))
```

Disabling the grammar suggestions... like whore i can spell tyvm

``` commonlisp
(after! company
  (add-hook! 'text-mode-hook (company-mode -1)))
```

AND FINALLY, FIXING ORG-MODES FUCKED CODE BLOCK DEFAULTS... BANE OF MY
LIFE THOSE LITTLE SHITS

``` commonlisp
(defun +yas/org-src-header-p ()
  "Determine whether `point' is within a src-block header or header-args."
  (pcase (org-element-type (org-element-context))
    ('src-block (< (point) ; before code part of the src-block
                   (save-excursion (goto-char (org-element-property :begin (org-element-context)))
                                   (forward-line 1)
                                   (point))))
    ('inline-src-block (< (point) ; before code part of the inline-src-block
                          (save-excursion (goto-char (org-element-property :begin (org-element-context)))
                                          (search-forward "]{")
                                          (point))))
    ('keyword (string-match-p "^header-args" (org-element-property :value (org-element-context))))))
```

And now a function to use yasnippets to produce a nice way to do header
args

``` commonlisp
(defun +yas/org-prompt-header-arg (arg question values)
  "Prompt the user to set ARG header property to one of VALUES with QUESTION.
The default value is identified and indicated. If either default is selected,
or no selection is made: nil is returned."
  (let* ((src-block-p (not (looking-back "^#\\+property:[ \t]+header-args:.*" (line-beginning-position))))
         (default
           (or
            (cdr (assoc arg
                        (if src-block-p
                            (nth 2 (org-babel-get-src-block-info t))
                          (org-babel-merge-params
                           org-babel-default-header-args
                           (let ((lang-headers
                                  (intern (concat "org-babel-default-header-args:"
                                                  (+yas/org-src-lang)))))
                             (when (boundp lang-headers) (eval lang-headers t)))))))
            ""))
         default-value)
    (setq values (mapcar
                  (lambda (value)
                    (if (string-match-p (regexp-quote value) default)
                        (setq default-value
                              (concat value " "
                                      (propertize "(default)" 'face 'font-lock-doc-face)))
                      value))
                  values))
    (let ((selection (consult--read question values :default default-value)))
      (unless (or (string-match-p "(default)$" selection)
                  (string= "" selection))
        selection))))
```

Finally, fetching the language info for the new source blocks Also,
providing a way for the most popular language in the buffer (with
`#+propertieos`)

``` commonlisp
(defun +yas/org-src-lang ()
  "Try to find the current language of the src/header at `point'.
Return nil otherwise."
  (let ((context (org-element-context)))
    (pcase (org-element-type context)
      ('src-block (org-element-property :language context))
      ('inline-src-block (org-element-property :language context))
      ('keyword (when (string-match "^header-args:\\([^ ]+\\)" (org-element-property :value context))
                  (match-string 1 (org-element-property :value context)))))))

(defun +yas/org-last-src-lang ()
  "Return the language of the last src-block, if it exists."
  (save-excursion
    (beginning-of-line)
    (when (re-search-backward "^[ \t]*#\\+begin_src" nil t)
      (org-element-property :language (org-element-context)))))

(defun +yas/org-most-common-no-property-lang ()
  "Find the lang with the most source blocks that has no global header-args, else nil."
  (let (src-langs header-langs)
    (save-excursion
      (goto-char (point-min))
      (while (re-search-forward "^[ \t]*#\\+begin_src" nil t)
        (push (+yas/org-src-lang) src-langs))
      (goto-char (point-min))
      (while (re-search-forward "^[ \t]*#\\+property: +header-args" nil t)
        (push (+yas/org-src-lang) header-langs)))

    (setq src-langs
          (mapcar #'car
                  ;; sort alist by frequency (desc.)
                  (sort
                   ;; generate alist with form (value . frequency)
                   (cl-loop for (n . m) in (seq-group-by #'identity src-langs)
                            collect (cons n (length m)))
                   (lambda (a b) (> (cdr a) (cdr b))))))

    (car (cl-set-difference src-langs header-langs :test #'string=))))
```

Lets also include \<\< to autocomplete, as with () and {}

``` commonlisp
(sp-local-pair
 '(org-mode)
 "<<" ">>"
 :actions '(insert))
```

And lastly lets add some helpful snippets for org-mode, and add a better
templete

``` elisp
(set-file-template! "\\.org$" :trigger "__" :mode 'org-mode)
```

## Defaults

Emacs has a lot of stupid defaults... Lets fix some!

``` commonlisp
(setq evil-want-fine-undo t
      scroll-margin 2
      display-line-numbers-type nil
      history-length 25
      browse-url-browser-function 'xwidget-webkit-browse-url
      truncate-string-ellipsis "...")

(fringe-mode 0)
(global-subword-mode 1)
```

Fixes an issue with flickering on wayland

``` commonlisp
(add-to-list 'default-frame-alist '(inhibit-double-buffering . t))
```

lisp-interaction-mode instead of fundemental mode

``` commonlisp
(setq doom-scratch-initial-major-mode 'lisp-interaction-mode)
```

Ask where to open splits, and open a buffer for it

``` commonlisp
(setq evil-vsplit-window-right t
      evil-split-window-below t)
(defadvice! prompt-for-buffer (&rest _)
  :after '(evil-window-split evil-window-vsplit)
  (consult-buffer))
```

Use `;` instead of `:` for entering command mode

``` commonlisp
(after! evil
  (map! :nmv ";" #'evil-ex)
  (map! :nmv ":" #'evil-repeat-find-char))
```

Disable the window divider to help emacs look a little bit cleaner

``` commonlisp
(custom-set-faces!
  `(vertical-border :background ,(doom-color 'bg) :foreground ,(doom-color 'bg)))

(when (boundp 'window-divider-mode)
  (setq window-divider-default-places nil
        window-divider-default-bottom-width 0
        window-divider-default-right-width 0)
  (window-divider-mode -1))
```

``` commonlisp
(set-frame-parameter nil 'internal-border-width 35)
(setq-default line-spacing 0.35)
```

``` commonlisp
(setq solaire-mode-real-buffer-fn
      (lambda ()
        (or (eq major-mode '+doom-dashboard-mode)
            (solaire-mode-real-buffer-p))))
```

``` commonlisp
(remove-hook 'doom-first-buffer-hook #'global-hl-line-mode)
```

## Visual Configuration

## Modeline

Techosaurs improvements

``` commonlisp
(after! doom-modeline
  (doom-modeline-def-segment buffer-name
    "Display the current buffer's name, without any other information."
    (concat
     (doom-modeline-spc)
     (doom-modeline--buffer-name)))

  (doom-modeline-def-segment pdf-icon
    "PDF icon from all-the-icons."
    (concat
     (doom-modeline-spc)
     (doom-modeline-icon 'octicon "file-pdf" nil nil
                         :face (if (doom-modeline--active)
                                   'all-the-icons-red
                                 'mode-line-inactive)
                         :v-adjust 0.02)))

  (defun doom-modeline-update-pdf-pages ()
    "Update PDF pages."
    (setq doom-modeline--pdf-pages
          (let ((current-page-str (number-to-string (eval `(pdf-view-current-page))))
                (total-page-str (number-to-string (pdf-cache-number-of-pages))))
            (concat
             (propertize
              (concat (make-string (- (length total-page-str) (length current-page-str)) ? )
                      " P" current-page-str)
              'face 'mode-line)
             (propertize (concat "/" total-page-str) 'face 'doom-modeline-buffer-minor-mode)))))

  (doom-modeline-def-segment pdf-pages
    "Display PDF pages."
    (if (doom-modeline--active) doom-modeline--pdf-pages
      (propertize doom-modeline--pdf-pages 'face 'mode-line-inactive)))

  (doom-modeline-def-modeline 'pdf
    '(bar window-number pdf-pages pdf-icon buffer-name)
    '(misc-info matches major-mode process vcs)))

```

Lets add some stuff to the modeline

``` elisp
(after! doom-modeline
  (display-time-mode 1)                              ;Enable time in the mode-line
  (setq doom-modeline-major-mode-icon t              ;Show major mode name
        doom-modeline-enable-word-count t            ;Show word count
        doom-modeline-modal-icon t                   ;Show vim mode icon
        inhibit-compacting-font-caches t))           ;Don't compact font caches in gc
```

The encoding is always utf-8, so this is a bit redundant, and i dont
realy like it.. Lets remove that

``` commonlisp
(defun doom-modeline-conditional-buffer-encoding ()
  "We expect the encoding to be LF UTF-8, so only show the modeline when this is not the case"
  (setq-local doom-modeline-buffer-encoding
              (unless (and (memq (plist-get (coding-system-plist buffer-file-coding-system) :category)
                                 '(coding-category-undecided coding-category-utf-8))
                           (not (memq (coding-system-eol-type buffer-file-coding-system) '(1 2))))
                t)))
(add-hook 'after-change-major-mode-hook #'doom-modeline-conditional-buffer-encoding) ;;remove encoding
```

## Centaur tabs

Hide the tabs if theres only one left

``` commonlisp
(defun centaur-tabs-get-total-tab-length ()
  (length (centaur-tabs-tabs (centaur-tabs-current-tabset))))

(defun centaur-tabs-hide-on-window-change ()
  (run-at-time nil nil
               (lambda ()
                 (centaur-tabs-hide-check (centaur-tabs-get-total-tab-length)))))

(defun centaur-tabs-hide-check (len)
  (shut-up
    (cond
     ((and (= len 1) (not (centaur-tabs-local-mode))) (call-interactively #'centaur-tabs-local-mode))
     ((and (>= len 2) (centaur-tabs-local-mode)) (call-interactively #'centaur-tabs-local-mode)))))

```

And have some nice icon stuff

``` commonlisp
(after! centaur-tabs
  (centaur-tabs-mode -1)
  (setq centaur-tabs-height 20
        centaur-tabs-set-icons t
        centaur-tabs-gray-out-icons 'buffer)
  (add-hook 'window-configuration-change-hook 'centaur-tabs-hide-on-window-change)
  (centaur-tabs-change-fonts "Iosevka Nerd Font" 105))
```

## Treemacs

``` commonlisp
(setq treemacs-width 25)
(setq doom-themes-treemacs-theme "doom-colors")
```

## Dashboard

Make a nice looking image be there because... yes

``` commonlisp
(defvar fancy-splash-image-template
  (expand-file-name "misc/splash-images/emacs-logo.svg" doom-private-dir)
  "Default template svg used for the splash image, with substitutions from ")

(defvar fancy-splash-sizes
  `((:height 300 :min-height 50 :padding (0 . 2))
    (:height 250 :min-height 42 :padding (2 . 4))
    (:height 200 :min-height 35 :padding (3 . 3))
    (:height 150 :min-height 28 :padding (3 . 3))
    (:height 100 :min-height 20 :padding (2 . 2))
    (:height 75  :min-height 15 :padding (2 . 1))
    (:height 50  :min-height 10 :padding (1 . 0))
    (:height 1   :min-height 0  :padding (0 . 0)))
  "list of plists with the following properties
  :height the height of the image
  :min-height minimum `frame-height' for image
  :padding `+doom-dashboard-banner-padding' (top . bottom) to apply
  :template non-default template file
  :file file to use instead of template")

(defvar fancy-splash-template-colours
  '(("$colour1" . keywords) ("$colour2" . type) ("$colour3" . base5) ("$colour4" . base8))
  "list of colour-replacement alists of the form (\"$placeholder\" . 'theme-colour) which applied the template")

(unless (file-exists-p (expand-file-name "theme-splashes" doom-cache-dir))
  (make-directory (expand-file-name "theme-splashes" doom-cache-dir) t))

(defun fancy-splash-filename (theme-name height)
  (expand-file-name (concat (file-name-as-directory "theme-splashes")
                            theme-name
                            "-" (number-to-string height) ".svg")
                    doom-cache-dir))

(defun fancy-splash-clear-cache ()
  "Delete all cached fancy splash images"
  (interactive)
  (delete-directory (expand-file-name "theme-splashes" doom-cache-dir) t)
  (message "Cache cleared!"))

(defun fancy-splash-generate-image (template height)
  "Read TEMPLATE and create an image if HEIGHT with colour substitutions as
   described by `fancy-splash-template-colours' for the current theme"
  (with-temp-buffer
    (insert-file-contents template)
    (re-search-forward "$height" nil t)
    (replace-match (number-to-string height) nil nil)
    (dolist (substitution fancy-splash-template-colours)
      (goto-char (point-min))
      (while (re-search-forward (car substitution) nil t)
        (replace-match (doom-color (cdr substitution)) nil nil)))
    (write-region nil nil
                  (fancy-splash-filename (symbol-name doom-theme) height) nil nil)))

(defun fancy-splash-generate-images ()
  "Perform `fancy-splash-generate-image' in bulk"
  (dolist (size fancy-splash-sizes)
    (unless (plist-get size :file)
      (fancy-splash-generate-image (or (plist-get size :template)
                                       fancy-splash-image-template)
                                   (plist-get size :height)))))

(defun ensure-theme-splash-images-exist (&optional height)
  (unless (file-exists-p (fancy-splash-filename
                          (symbol-name doom-theme)
                          (or height
                              (plist-get (car fancy-splash-sizes) :height))))

    (fancy-splash-generate-images)))

(defun get-appropriate-splash ()
  (let ((height (frame-height)))
    (cl-some (lambda (size) (when (>= height (plist-get size :min-height)) size))
             fancy-splash-sizes)))

(setq fancy-splash-last-size nil)
(setq fancy-splash-last-theme nil)
(defun set-appropriate-splash (&rest _)
  (let ((appropriate-image (get-appropriate-splash)))
    (unless (and (equal appropriate-image fancy-splash-last-size)
                 (equal doom-theme fancy-splash-last-theme)))
    (unless (plist-get appropriate-image :file)
      (ensure-theme-splash-images-exist (plist-get appropriate-image :height)))
    (setq fancy-splash-image
          (or (plist-get appropriate-image :file)
              (fancy-splash-filename (symbol-name doom-theme) (plist-get appropriate-image :height))))
    (setq +doom-dashboard-banner-padding (plist-get appropriate-image :padding))
    (setq fancy-splash-last-size appropriate-image)
    (setq fancy-splash-last-theme doom-theme)
    (+doom-dashboard-reload)))

(add-hook 'window-size-change-functions #'set-appropriate-splash)
(add-hook 'doom-load-theme-hook #'set-appropriate-splash)
```

And lets add a nice little phrasey thingy in too

``` commonlisp
(defvar splash-phrase-source-folder
  (expand-file-name "misc/splash-phrases" doom-private-dir)
  "A folder of text files with a fun phrase on each line.")

(defvar splash-phrase-sources
  (let* ((files (directory-files splash-phrase-source-folder nil "\\.txt\\'"))
         (sets (delete-dups (mapcar
                             (lambda (file)
                               (replace-regexp-in-string "\\(?:-[0-9]+-\\w+\\)?\\.txt" "" file))
                             files))))
    (mapcar (lambda (sset)
              (cons sset
                    (delq nil (mapcar
                               (lambda (file)
                                 (when (string-match-p (regexp-quote sset) file)
                                   file))
                               files))))
            sets))
  "A list of cons giving the phrase set name, and a list of files which contain phrase components.")

(defvar splash-phrase-set
  (nth (random (length splash-phrase-sources)) (mapcar #'car splash-phrase-sources))
  "The default phrase set. See `splash-phrase-sources'.")

(defun splase-phrase-set-random-set ()
  "Set a new random splash phrase set."
  (interactive)
  (setq splash-phrase-set
        (nth (random (1- (length splash-phrase-sources)))
             (cl-set-difference (mapcar #'car splash-phrase-sources) (list splash-phrase-set))))
  (+doom-dashboard-reload t))

(defvar splase-phrase--cache nil)

(defun splash-phrase-get-from-file (file)
  "Fetch a random line from FILE."
  (let ((lines (or (cdr (assoc file splase-phrase--cache))
                   (cdar (push (cons file
                                     (with-temp-buffer
                                       (insert-file-contents (expand-file-name file splash-phrase-source-folder))
                                       (split-string (string-trim (buffer-string)) "\n")))
                               splase-phrase--cache)))))
    (nth (random (length lines)) lines)))

(defun splash-phrase (&optional set)
  "Construct a splash phrase from SET. See `splash-phrase-sources'."
  (mapconcat
   #'splash-phrase-get-from-file
   (cdr (assoc (or set splash-phrase-set) splash-phrase-sources))
   " "))

(defun doom-dashboard-phrase ()
  "Get a splash phrase, flow it over multiple lines as needed, and make fontify it."
  (mapconcat
   (lambda (line)
     (+doom-dashboard--center
      +doom-dashboard--width
      (with-temp-buffer
        (insert-text-button
         line
         'action
         (lambda (_) (+doom-dashboard-reload t))
         'face 'doom-dashboard-menu-title
         'mouse-face 'doom-dashboard-menu-title
         'help-echo "Random phrase"
         'follow-link t)
        (buffer-string))))
   (split-string
    (with-temp-buffer
      (insert (splash-phrase))
      (setq fill-column (min 70 (/ (* 2 (window-width)) 3)))
      (fill-region (point-min) (point-max))
      (buffer-string))
    "\n")
   "\n"))

(defadvice! doom-dashboard-widget-loaded-with-phrase ()
  :override #'doom-dashboard-widget-loaded
  (setq line-spacing 0.2)
  (insert
   "\n\n"
   (propertize
    (+doom-dashboard--center
     +doom-dashboard--width
     (doom-display-benchmark-h 'return))
    'face 'doom-dashboard-loaded)
   "\n"
   (doom-dashboard-phrase)
   "\n"))
```

Lastly, the doom dashboard \"useful commands\" are no longer useful to
me. So, we\'ll disable them and then for a particularly *clean* look
disable the modeline, then also hide the cursor.

``` commonlisp
(remove-hook '+doom-dashboard-functions #'doom-dashboard-widget-shortmenu)
(add-hook! '+doom-dashboard-mode-hook (hide-mode-line-mode 1) (hl-line-mode -1))
(setq-hook! '+doom-dashboard-mode-hook evil-normal-state-cursor (list nil))
```

Turning off solaire so that it doesn\'t look ugly

``` commonlisp
(add-hook '+doom-dashboard-mode-hook #'turn-off-solaire-mode)
```

## Writeroom

Some nice asthetic tweaks when using org-mode with writeroom-mode
enabled. Namely:

-   Use a serif-ed variable-pitch font
-   Hiding headline leading stars
-   Using fleurons as headline bullets
-   Hiding line numbers
-   Removing outline indentation
-   Centering the text
-   Turning on `org-pretty-table-mode`
-   Disabling `doom-modeline`

``` commonlisp
(defvar +zen-serif-p t
  "Whether to use a serifed font with `mixed-pitch-mode'.")
(after! writeroom-mode
  (defvar-local +zen--original-org-indent-mode-p nil)
  (defvar-local +zen--original-mixed-pitch-mode-p nil)
  (defun +zen-enable-mixed-pitch-mode-h ()
    "Enable `mixed-pitch-mode' when in `+zen-mixed-pitch-modes'."
    (when (apply #'derived-mode-p +zen-mixed-pitch-modes)
      (if writeroom-mode
          (progn
            (setq +zen--original-mixed-pitch-mode-p mixed-pitch-mode)
            (funcall (if +zen-serif-p #'mixed-pitch-serif-mode #'mixed-pitch-mode) 1))
        (funcall #'mixed-pitch-mode (if +zen--original-mixed-pitch-mode-p 1 -1)))))
  (pushnew! writeroom--local-variables
            'display-line-numbers
            'visual-fill-column-width
            'org-adapt-indentation
            'org-superstar-headline-bullets-list
            'org-superstar-remove-leading-stars)
  (add-hook 'writeroom-mode-enable-hook
            (defun +zen-prose-org-h ()
              "Reformat the current Org buffer appearance for prose."
              (when (eq major-mode 'org-mode)
                (setq display-line-numbers nil
                      visual-fill-column-width 60
                      org-adapt-indentation nil)
                (when (featurep 'org-superstar)
                  (setq-local org-superstar-headline-bullets-list '("◉" "○" "✸" "✿" "✤" "✜" "◆" "▶")
                              org-superstar-remove-leading-stars t)
                  (org-superstar-restart))               (setq
                 +zen--original-org-indent-mode-p org-indent-mode)
                (org-indent-mode -1))))
  (add-hook! 'writeroom-mode-hook
    (if writeroom-mode
        (add-hook 'post-command-hook #'recenter nil t)
      (remove-hook 'post-command-hook #'recenter t)))
  (add-hook 'writeroom-mode-enable-hook #'doom-disable-line-numbers-h)
  (add-hook 'writeroom-mode-disable-hook #'doom-enable-line-numbers-h)
  (add-hook 'writeroom-mode-disable-hook
            (defun +zen-nonprose-org-h ()
              "Reverse the effect of `+zen-prose-org'."
              (when (eq major-mode 'org-mode)
                (when (featurep 'org-superstar)
                  (org-superstar-restart))
                (when +zen--original-org-indent-mode-p (org-indent-mode 1))))))
```

## Font display

`+org-pretty-mode` is awesome!

``` commonlisp
(setq org-pretty-entities-include-sub-superscripts nil)
```

And lets make headings a bit bigger so they stand out more

``` commonlisp
(custom-set-faces!
  '(org-document-title :height 1.2)
  '(outline-1 :weight extra-bold :height 1.25)
  '(outline-2 :weight bold :height 1.15)
  '(outline-3 :weight bold :height 1.12)
  '(outline-4 :weight semi-bold :height 1.09)
  '(outline-5 :weight semi-bold :height 1.06)
  '(outline-6 :weight semi-bold :height 1.03)
  '(outline-8 :weight semi-bold)
  '(outline-9 :weight semi-bold))
```

It seems reasonable to have deadlines in the error face when they\'re
passed.

``` commonlisp
(setq org-agenda-deadline-faces
      '((1.0 . error)
        (1.0 . org-warning)
        (0.5 . org-upcoming-deadline)
        (0.0 . org-upcoming-distant-deadline)))
```

We can then have quote blocks stand out a bit more by making them
*italic*.

``` commonlisp
(setq org-fontify-quote-and-verse-blocks t)
```

``` commonlisp
(use-package! org-appear
  :hook (org-mode . org-appear-mode)
  :config
  (setq org-appear-autoemphasis t
        org-appear-autosubmarkers t
        org-appear-autolinks nil)
  (run-at-time nil nil #'org-appear--set-elements))
```

Org files can be rather nice to look at, particularly with some of the
customisations here. This comes at a cost however, expensive font-lock.
Feeling like you\'re typing through molasses in large files is no fun,
but there is a way I can defer font-locking when typing to make the
experience more responsive.

``` commonlisp
(defun locally-defer-font-lock ()
  "Set jit-lock defer and stealth, when buffer is over a certain size."
  (when (> (buffer-size) 50000)
    (setq-local jit-lock-defer-time 0.05
                jit-lock-stealth-time 1)))

(add-hook 'org-mode-hook #'locally-defer-font-lock)


(custom-set-faces!
  `(org-block-end-line :background ,(doom-color 'base2))
  `(org-block-begin-line :background ,(doom-color 'base2)))
```

### Fontifying inline source blocks

Ah god... I quote some random config

> Org does lovely things with `#+begin_src`{.verbatim} blocks, like
> using font-lock for language\'s major-mode behind the scenes and
> pulling out the lovely colourful results. By contrast, inline
> `src_`{.verbatim} blocks are somewhat neglected.
>
> I am not the first person to feel this way, thankfully others have
> [taken to
> stackexchange](https://stackoverflow.com/questions/20309842/how-to-syntax-highlight-for-org-mode-inline-source-code-src-lang/28059832)
> to voice their desire for inline src fontification. I was going to
> steal their work, but unfortunately they didn\'t perform *true* source
> code fontification, but simply applied the `org-code`{.verbatim} face
> to the content.
>
> We can do better than that, and we shall! Using
> `org-src-font-lock-fontify-block` we can apply language-appropriate
> syntax highlighting. Then, continuing on to
> `{{{results(...)}}}`{.verbatim} , it can have the
> `org-block`{.verbatim} face applied to match, and then the
> value-surrounding constructs hidden by mimicking the behaviour of
> `prettify-symbols-mode`.

Now, i wholly agree with this. But icba to explain it

``` commonlisp
(defvar org-prettify-inline-results t
  "Whether to use (ab)use prettify-symbols-mode on {{{results(...)}}}.
Either t or a cons cell of strings which are used as substitutions
for the start and end of inline results, respectively.")

(defvar org-fontify-inline-src-blocks-max-length 200
  "Maximum content length of an inline src block that will be fontified.")

(defun org-fontify-inline-src-blocks (limit)
  "Try to apply `org-fontify-inline-src-blocks-1'."
  (condition-case nil
      (org-fontify-inline-src-blocks-1 limit)
    (error (message "Org mode fontification error in %S at %d"
                    (current-buffer)
                    (line-number-at-pos)))))

(defun org-fontify-inline-src-blocks-1 (limit)
  "Fontify inline src_LANG blocks, from `point' up to LIMIT."
  (let ((case-fold-search t)
        (initial-point (point)))
    (while (re-search-forward "\\_<src_\\([^ \t\n[{]+\\)[{[]?" limit t) ; stolen from `org-element-inline-src-block-parser'
      (let ((beg (match-beginning 0))
            pt
            (lang-beg (match-beginning 1))
            (lang-end (match-end 1)))
        (remove-text-properties beg lang-end '(face nil))
        (font-lock-append-text-property lang-beg lang-end 'face 'org-meta-line)
        (font-lock-append-text-property beg lang-beg 'face 'shadow)
        (font-lock-append-text-property beg lang-end 'face 'org-block)
        (setq pt (goto-char lang-end))
        ;; `org-element--parse-paired-brackets' doesn't take a limit, so to
        ;; prevent it searching the entire rest of the buffer we temporarily
        ;; narrow the active region.
        (save-restriction
          (narrow-to-region beg (min (point-max) limit (+ lang-end org-fontify-inline-src-blocks-max-length)))
          (when (ignore-errors (org-element--parse-paired-brackets ?\[))
            (remove-text-properties pt (point) '(face nil))
            (font-lock-append-text-property pt (point) 'face 'org-block)
            (setq pt (point)))
          (when (ignore-errors (org-element--parse-paired-brackets ?\{))
            (remove-text-properties pt (point) '(face nil))
            (font-lock-append-text-property pt (1+ pt) 'face '(org-block shadow))
            (unless (= (1+ pt) (1- (point)))
              (if org-src-fontify-natively
                  (org-src-font-lock-fontify-block (buffer-substring-no-properties lang-beg lang-end) (1+ pt) (1- (point)))
                (font-lock-append-text-property (1+ pt) (1- (point)) 'face 'org-block)))
            (font-lock-append-text-property (1- (point)) (point) 'face '(org-block shadow))
            (setq pt (point))))
        (when (and org-prettify-inline-results (re-search-forward "\\= {{{results(" limit t))
          (font-lock-append-text-property pt (1+ pt) 'face 'org-block)
          (goto-char pt))))
    (when org-prettify-inline-results
      (goto-char initial-point)
      (org-fontify-inline-src-results limit))))

(defun org-fontify-inline-src-results (limit)
  (while (re-search-forward "{{{results(\\(.+?\\))}}}" limit t)
    (remove-list-of-text-properties (match-beginning 0) (point)
                                    '(composition
                                      prettify-symbols-start
                                      prettify-symbols-end))
    (font-lock-append-text-property (match-beginning 0) (match-end 0) 'face 'org-block)
    (let ((start (match-beginning 0)) (end (match-beginning 1)))
      (with-silent-modifications
        (compose-region start end (if (eq org-prettify-inline-results t) "⟨" (car org-prettify-inline-results)))
        (add-text-properties start end `(prettify-symbols-start ,start prettify-symbols-end ,end))))
    (let ((start (match-end 1)) (end (point)))
      (with-silent-modifications
        (compose-region start end (if (eq org-prettify-inline-results t) "⟩" (cdr org-prettify-inline-results)))
        (add-text-properties start end `(prettify-symbols-start ,start prettify-symbols-end ,end))))))

(defun org-fontify-inline-src-blocks-enable ()
  "Add inline src fontification to font-lock in Org.
Must be run as part of `org-font-lock-set-keywords-hook'."
  (setq org-font-lock-extra-keywords
        (append org-font-lock-extra-keywords '((org-fontify-inline-src-blocks)))))

(add-hook 'org-font-lock-set-keywords-hook #'org-fontify-inline-src-blocks-enable)
```
