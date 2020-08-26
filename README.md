## Binary Clock

Binary clock with Svelte for fun. 

[Live here](https://nikals.se/binaryclock/)


### How it works

Every second it takes the current time, converts it, and displays it like a conventional binary clock, in decimal form but binary-encoded 10s and 1s.

[![](https://github.com/nikalsh/svelte-binary-clock/blob/master/screenshot.png?raw=true)](#)

To get the 1s from the time, use modulo 10. Then iterate over the bits with right-shift. Get the value of the current bit by doing bitwise AND (&) with 1.

*"time" is either hours, minutes or seconds*
```javascript
let oneBits = (time % 10);

    for (let i = 0; i < binaryClock[hand]["1"].length; i++) {
        binaryClock[hand]["1"][i] = oneBits & 1;
        oneBits >>= 1;
    }
```

To get the 10s just divide time by 10 and iterate over the bits again.
 

### Run it locally
```bash
npm install
npm run dev
```

### Build it
```bash
npm run build
```
