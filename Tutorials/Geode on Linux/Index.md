# How to install Geode on Linux

1. Download Geode Installer for **Windows** from the [official website](https://geode-sdk.org)
![Geode Main Page](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode1.png)
![Geode Download for Windows](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode2.png)

2. Install Geometry Dash (if you haven't yet)
![Steam Library with Geometry Dash installed](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode3.png)
![Steam Install Geometry Dash](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode4.png)

3. Click on the **Manage** button
![Steam Manage button](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode5.png)

4. Go to **Manage** > **Manage** > **Browse local files**
![Steam Browse local files](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode6.png)

5. Move the Geometry Dash folder to another folder. I moved it to the Downloads folder, for example.
![Geometry Dash folder in Downloads](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode7.png)

6. Make sure you have Wine installed. If not, you can follow [this](https://github.com/Jotalea/Jotalea/blob/main/Tutorials%2FWine%20on%20Linux%2FIndex.md) tutorial on how to install it.

7. Run the installer

8. Select the appropriate language, click **Ok**, then **Next**, **Agree**, **Next**

9. Click **Browse**

10. Search for the Geometry Dash folder you moved previously
![Geode Installer - Browse for Geometry Dash folder](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode8.png)
In my case, it's in the Downloads folder

11. Once selected, it should look like this
![Geode Installer with Geometry Dash folder selected](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geode9.png)

12. Click **Install** and wait for it to finish

13. Move the Geometry Dash folder back to the **Steam** folder (/home/user/.local/share/Steam/steamapps/common)
![Geometry Dash folder back in Steam directory](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geodeA.png)

14. Go back to Steam, then click the **Manage** icon > **Properties**
![Steam > Geometry Dash > Manage > Properties](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geodeB.png)

15. Paste this in the **Launch Options** textbox:
```WINEDLLOVERRIDES="XInput1_4=n,b" %command%```
![Wine DLL override flag](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geodeC.png)

16. **Launch** the game as usual
![Geometry Dash with Geode modloader installed](https://raw.githubusercontent.com/Jotalea/Jotalea/main/Tutorials/Geode%20on%20Linux/geodeD.png)

That's it, now you can install any mod available. If this helped you, I'd love that you star this repository.
