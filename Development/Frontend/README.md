## CSS
- id(#) vs class(.)
  - https://bangu4.tistory.com/26
---
## React
- class vs className
  - https://dream-frontend.tistory.com/254
- .env
  - process.env.REACT_APP_*
- hide sourcecode
  ```
  "scripts":{
    ...
    "build": "GENERATE_SOURCEMAP=false react-scripts build"
  }
  ```
---
## Github Pages
- npm i gh-pages
- set homepage, CNAME 
  ```
  "homepage": "https://*"
  "scripts":{
    ...
    "predeploy": "npm run build && cp CNAME ./build",
    "deploy": "gh-pages -d build"
  }
  ```
- `npm run deploy`
