# 🖌️ Distro Art

**File:** `distros.toml`

To create a new DistroArt object, add a new section to the file (replace `distroname` with the name of your distro):
```toml
[distroname]
```
 
Catnap's DistroArt objects have three possible keys.
1. `margin`
2. `art`
3. `alias`

## Margin
The `margin` key is used to define the top, left and right margins of the art. For example:

> *Art with `margin = [0, 0, 0]`*
```txt  
      /\      ╭────────────╮
     /  \     │ > uptime   │
    /\   \    │ > distro   │
   /      \   │ > shell    │
  /   ,,   \  │ > disk1    │
 /   |  |  -\ │ > disk2    │  
/_-''    ''-_\╰────────────╯
```

> *Art with `margin = [3, 3, 3]`*
```txt 
                   ╭────────────╮        
                   │ > uptime   │   
                   │ > distro   │    
          /\       │ > shell    │
         /  \      │ > disk1    │
        /\   \     │ > disk2    │
       /      \    ╰────────────╯
      /   ,,   \  
     /   |  |  -\   
    /_-''    ''-_\
```

## Art
The `art` key is used to define the ASCII-art for your distro.
For example:
```
art = [
  "Test",
  "Test",
  "Test"
]
```

## Alias
The `alias` key can be used to define alternate names that should also refer to the DistroArt Object.

*Example in which 'test1' also refers to your new DistroArt object:*
```
alias = "test1"
```

This is also used to define the `default` DistroArt object, which defines what art should be displayed by default.

To add more then one alias to an Distroart object, you can separate them by comma.

## Example DistroArt object
```toml
[distroart.test]
alias = "test1"
margin = [3, 3 ,3]
art = [
  "Test",
  "Test",
  "Test"
]
```
