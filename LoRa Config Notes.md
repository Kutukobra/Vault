
```
#define LORA_FREQ 433E6
#define LORA_SYNCWORD 0x67
#define LORA_CODINGRATE 5
#define LORA_SPREADINGFACTOR 7
#define LORA_BANDWIDTH 125E3
#define LORA_POWER 17
#define LORA_PREAMBLE 6
#define LORA_GAIN 0
```
![[Pasted image 20261009145219.png]]
# Coding Rate
- CR = 4
  Fine, no noticeable change
## Spreading Factor
- SF = 6
  Data gone
- SF = 12
  Still gone
- SF = 9
  Slow as hell. Distance basically the same. Not worth it.
- SF = 7
  Default
## Bandwidth
- BW = 500E3
  Way faster. A lot of missing data.
- BW = 250E3
  Slightly faster. Not as much missing data.