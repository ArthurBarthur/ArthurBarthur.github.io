# Jon Arthur Marrable
<img src="stuff/photo.jpg" width="35%" alt="Hei!" class="inline"/>

## Technical implementation (interactive 3d)
- Synthesis/DSP
- Physical audio propagation
- Procedural generation (music, VFX, systems)
- AR/VR/MR/xR
- Everything related to Unreal Engine

## Dev-Ops
- Large scale cloud infrastructure monitoring
- LAN/WAN network design & optimization
- Web back-end (hosting, DNS, https/certificates/encryption, official registrar role, load-balancing, netsec, ++++++)
- Virtualization
- Trend analysis
- Automation (deep-layered SLA reports, anyone?)
- Disaster-recovery
- Project coordination/ownership
- Global operations


Experiments in interactive 3D domain | Video Links
------------ | -------------
Acoustic Spa Experience | [Youtube](https://youtu.be/Sf01NNtXoS8)
Music Visualizer "Candy" | [Youtube](https://youtu.be/5Hb8X3R4TWY)
Music Visualizer "Rocket" | [Youtube](https://youtu.be/m6ZYMHoDMBQ)
Soft-Loop exploring | [Youtube](https://youtu.be/Xr4OubfF4RE)
Rube Goldberg-esque interactive melody machine | [Youtube](https://youtu.be/Ha2dC7se8yA)
Synthwave synthesizer car | [Youtube](https://youtu.be/sgXgEhou9Kg)



C# example where I generate different wavetypes inside Unitys audio-thread, writing directly to audiobuffer(wave oscillators are the base noise-generators in a synthesizer):
```cs
    //AUDIOTHREAD
    void OnAudioFilterRead(float[] data, int channels)
    {
       //find audio tick delta inside audio thread
        currentDSPtime = AudioSettings.dspTime;
        deltaDSPtime = currentDSPtime - lastDSPtime;
        lastDSPtime = currentDSPtime;
        // update increment in case frequency has changed
        increment = actualFrequency * 2.0 * System.Math.PI / sampling_frequency;
        //triangle helper
        double trianglehelp = actualFrequency * 2.0 / sampling_frequency;
            for (var i = 0; i < data.Length; i = i + channels)
            {
                phase = phase + increment;
            //select wave type
            switch (_wavetypeenmumfromchord)
                {
                    case ChordSpawner.WaveTypesSelector.Sine:
                    //generate sine wave
                    data[i] = (float)(System.Math.Sin(phase));
                    break;
                    case ChordSpawner.WaveTypesSelector.Triangle:
                    //generate triangle wave
                    double div = i * trianglehelp;
                        data[i] = (float)(((((int)div) % 2 == 0) ? -finalOscGain : finalOscGain) * (1.0 - 2.0 * (div - (int)div)));
                    break;
                    case ChordSpawner.WaveTypesSelector.Square:
                    //generate square wave
                    data[i] = Mathf.Sign(Mathf.Sin((float)phase * 2f * Mathf.PI));
                    break;
                    case ChordSpawner.WaveTypesSelector.Noise:
                    //generate noise wave
                    data[i] = offset - 1.0f + (float)randomNumber.NextDouble() * 2.0f;
                    break;
                }
                //make sure channel-summing doesn't blow stuff up
                if (channels == 2) data[i + 1] = data[i];
                //reset out-of-bounds wave-phase
                if (phase > 2 * System.Math.PI) phase = 0;
            }
        //send frequency changes async, from gamethread
        frequency = Mathf.MoveTowards(frequency, newFrequency, ((frequency + newFrequency) * (1 / noteLerpSpeedInSec)) * (float)deltaDSPtime);
        actualFrequency = frequency;
    }
```

### Contact

marrable@gmail.com

