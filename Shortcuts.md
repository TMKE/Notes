#### Notion  
- `shift` + `enter` go to new line in the same paragraph  
#### VSCode  
- hold alt and move a line up or down using arrows  
* `ctrl+d` to select word, then `ctrl+shift+l` to select multiple occurrences  
#### Linux  
* Writing a :colon: in app search shows shut down menu  
### Windows  
* Hold `shift` while dragging a window to put it in a fancy zone  
* Press `alt` to view accessibility option and navigate using the first letter  
* Press `alt` + `space` and select `move` to move a window using arrows  
* Press `alt` + `ctrl` + `space` to open PowerToys Run  
#### Vim  
- `:open FILE\_PATH\`   
- Splitting screen:  
	- vertically: `ctrl` + `w` then `v` or `:vsplit`
	- horizontally: `ctrl` + `w` then `s` 
	- `:split filename`: split window and load another file
	- Change the split screen window size:  
		- increase width: `ctrl` + `w` then `>`  
		- decrease width: `ctrl` + `w` then `<`  
		- increase height: `ctrl` + `w` then `+`  
		- decrease height: `ctrl` + `w` then `-`  
		- reset: `ctrl` + `w` then `=`  
	- Switch between windows:  
		- toggle between open windows: `ctrl` + `w` then `w`  
		- move to *left/bottom/top/right* window accordingly: `ctrl` + `w` then `h/j/k/l`  
	- Swap two parts of a split window: `ctrl` + `w` then `ctrl` + `r`  
	- New tab: `:tabnew`  
	- Switching between tabs:  
		- next tab: `gt`  
		- Prior tab: `gT`  
		- tab one: `1gt`  
		- tab two: `2gt` etc.  
	- Remap keybindings: `nnoremap <new> <old>` (in `.vimrc`)  
	- Open horizontal terminal: `:term`  
	   - Open vertical terminal: `:vert term`  
	- Go to external terminal real quick:  
		1- pause Vim using `ctrl` + `z`  
		2- execute the commands  
		3- return to Vim by typing the command `fg`  
		(alternatively, you can use `:sh` and remap it to `ctrl` + `d` to toggle quickly between `sh` and Vim)
- `:e filename`: edit another file
- `:mks ~/.vim/sessions/session1.vim`: save your current workspace (the layout of your windows)
- `:source ~/.vim/sessions/session1.vim`: Restore the session
	- Or from the terminal: `vim -S ~/.vim/sessions/session1.vim`
- `:mks!`: override the session
- `:qa`: quit all open buffers, splits, and tabs
- `:wqall`: write changes before closing
- `:only`: keep only this window open
- Moving windows:
	- `Ctrl` + `w`: enter "windows command mode":
		- \+ `R`: rotate windows up/left
		- \+ `r`: rotate windows down/right
		- \+ `L`/`H`: move current window to the far right/left
		- \+ `K`/`J`: move current window to the very top/bottom