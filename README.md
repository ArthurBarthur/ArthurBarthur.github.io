# Jon Arthur Marrable
<img src="stuff/photo.jpg" width="35%" alt="Hei!" class="inline"/>

## Technical implementation
- synthesis/DSP
- 3D audio propagation
- procedural generation (music, VFX, systems)
- AR/VR/MR/xR


Experiment | Video Link
------------ | -------------
Soft-Loop exploring | [Youtube](https://youtu.be/Xr4OubfF4RE)
Rube Goldberg-esque interactive melody machine | [Link](https://youtu.be/Ha2dC7se8yA)
Synthwave synthesizer car | [Youtube](https://youtu.be/sgXgEhou9Kg)
Music Visualizer "Candy" | [Youtube](https://youtu.be/5Hb8X3R4TWY)
Music Visualizer "Rocket" | [Youtube](https://youtu.be/m6ZYMHoDMBQ)

Creating different wavetypes and sending them directly to audiobuffer(base for a synthesizer):
```markdown
for (var i = 0; i < data.Length; i = i + channels)
            {
                phase = phase + increment;
                switch (_wavetypeenmumfromchord)                                                                                        //select wave type
                {
                    case ChordSpawner.WaveTypesSelector.Sine:
                        data[i] = (float)(System.Math.Sin(phase));                                                                      //generate sine wave
                    break;
                    case ChordSpawner.WaveTypesSelector.Triangle:
                        double div = i * trianglehelp;
                        data[i] = (float)(((((int)div) % 2 == 0) ? -finalOscGain : finalOscGain) * (1.0 - 2.0 * (div - (int)div)));     //generate triangle wave
                    break;
                    case ChordSpawner.WaveTypesSelector.Square:
                        data[i] = Mathf.Sign(Mathf.Sin((float)phase * 2f * Mathf.PI));                                                  //generate square wave
                    break;
                    case ChordSpawner.WaveTypesSelector.Noise:
                        data[i] = offset - 1.0f + (float)randomNumber.NextDouble() * 2.0f;                                              //generate noise wave
                    break;

                }
                if (channels == 2) data[i + 1] = data[i];
                if (phase > 2 * System.Math.PI) phase = 0;
            }
```

### Support or Contact

marrable@gmail.com

