# CS2053 -- Concept Assignment 2

## Due: 11:00pm, Wed., Feb. 10, 2020

## Instructions 
For this assignment, you should complete it in a Word document.Add "Concept Assignment 2", your name, student number and email at the top of the file. Please label the numbers clearly for each problem in your document. 

You may also like to answer some questions on paper (for example, when writing vectors) and scan them and insert them into your document. Microsoft Office Lens - Scanner is a useful app for your phone for this [Android](https://play.google.com/store/apps/details?id=com.microsoft.office.officelens&hl=en_CA&gl=US) and [iPhone](https://apps.apple.com/us/app/microsoft-office-lens-pdf-scan/id975925059).

## Questions 
Answer the following questions related to contents of Chapters 3 and 4 of the “Game Programming Algorithms and Techniques” book, the contents of our lecture and the contents of the Unity manual.

 1. Assume two game objects ```gameObject1``` and ```gameObject2``` in a 2D game.
    - a) Assume that ```gameObject1.position``` is (2, 2) and ```gameObject2.position``` is (8, 8), what is the vector vector that points from gameObject1 to ```gameObject2```?
    ````diff
    It's gameObject2.position - gameObject1.position = (6,6)
    ````
    - b) Write code to calculate direction from gameObject1’s position to gameObject2’s position using vector calculation.
        + Note that direction must be a normalized vector.
    ````csharp
    Vector3 arrowVector = Normalize(gameObject2.position - gameObject1.position);
    ````
 
 2. In lab assignments, we an program the motion of a game object in the ```update()``` method with the following code:

    ```csharp
        gameObjectPosition = gameObjectPosition + gameObjectMovement;
    ```

 where both gameObjectPosition and gameObjectMovement are 2D vectors.

 Assume that currently gameObjectPosition is at (1, 2) and gameObjectMovement is (3, 2), draw a figure to show the 3 vectors in X-Y axes:
    + The original gameObjectPosition vector
    + The gameObjectMovement vector
    + The updated gameObjectPosition vector
    ![alt text](https://github.com/CS-2053-Winter-2021/concept-assignment-2-RemLawrence/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20210210122450.png)

 3. You are coding a top-down 2D game with stereo sound. In a cut-scene you are scripting and explosion occurs. You must determine whether to play the sound in the right or left speaker depending on where the explosion has occurred relative to the character. Describe how you can solve this problem using vector math. Provide formulas to help explain your answer.
````diff
Use the length squared formula to determine the explosion is closer to player's left side or right side.
````
![alt text](https://github.com/CS-2053-Winter-2021/concept-assignment-2-RemLawrence/blob/master/2021_02_03_11n_Kleki.png)


 
 4. The following is the algorithm of Phong Reflection Model

    ```csharp
        // Vector3 N = normal of surface
        // Vector3 eye = position of camera
        // Vector3 pos = position on surface
        // float a = specular power (shininess)
        Vector3 V = Normalize(eye – pos) // FROM surface TO camera
        Vector3 Phong = AmbientColor
        foreach Light light in scene
           if light affects surface
              Vector3 L = Normalize(light.pos – pos)
              Phong += DiffuseColor * DotProduct(N, L)
              Vector3 R = Normalize(Reflect(-L, N)) // Reflect –L about N
              Phong += SpecularColor * pow(DotProduct(R, V), a)
           end
        end
    ```

     - a) Explain in ```Phong += DiffuseColor * DotProduct(N, L)```, what is the meaning of ```DotProduct(N, L)```? Why do we need to multiply value of “DotProduct(N, L)” with “DiffuseColor”? For a directional light without a light source position, what is L vector?
     ````diff
     The DotProduct(N, L) is gonna return the angle/scalar value of the vector from the surface to the light (L) and the normal of the surface.
     Multiply it by the DiffuseColor is to scale/adjust the brightness of the color on the surface (Diffuse component).         
     If is a directional light without a light source position (i.e the sun), the L represents the direction from the directional light (i.e the sun) to the object.
     ````
     - b) For ```Phong += SpecularColor * pow(DotProduct(R, V), a)```, what is meaning of ```DotProduct(R, V)```? Why we  need to multiply value of ```pow(DotProduct(R, V), a)``` with ```SpecularColor```?
     ````diff
     DotProduct(R, V) means to calculate the angle/scalar value of the vector from surface to camera and the reflection vector.
     To calculate the shining highlights on the surface (Specular component) relative to camera's position.
     ````


 5. The following is Z-Buffering algorithm:
    ```csharp
    // zBuffer[x][y] grabs depth at that pixel
    foreach Object o in scene
       foreach Pixel p in o
          float depth = calculate depth at p
          if zBuffer[p.x][p.y] > depth
             draw p
             zBuffer[p.x][p.y] = depth
          end
       end
    end
    ```

    Note that this algorithm is per-pixel based.

    - a) In terms of 4 coordination systems and their transformation stages: model -> world -> camera -> projection, in which coordination system should the z-buffer algorithm be applied? Explain your answer.
    ````diff
    The Z-buffering should be applied in projection stage, since the z-buffering algorithm itself is to determine which pixel to draw onto the screen which should happen in projection.
    ````
    - b) Given a pixel p of an object o, what is your idea to calculate this pixel’s depth? In which coordination system and/or transformation of 2 coordination systems?
    ````diff
    I guess you need to have an eye (position of camera) and then calculate the distance from the eye to the pixel in order to represent depth.
    Coordination system: Model Space and View/Camera Space
    ````

 6. Consider the following vectors: 
   
      ![](https://latex.codecogs.com/svg.latex?\Large&space;\vec{a}=\langle%203,4,2%20\rangle)

      ![](https://latex.codecogs.com/svg.latex?\Large&space;\vec{b}=\langle%206,8,0\rangle)
      
      and the scalar value: 
      
      ![](https://latex.codecogs.com/svg.latex?\Large&space;s=2)

    Calculate each of the following: 

      - a) ![](https://latex.codecogs.com/svg.latex?\Large&space;\vec{a}+\vec{b})
![alt text](https://github.com/CS-2053-Winter-2021/concept-assignment-2-RemLawrence/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20210208140956.png)

      - b) ![](https://latex.codecogs.com/svg.latex?\Large&space;s\cdot\vec{b})
![alt text](https://github.com/CS-2053-Winter-2021/concept-assignment-2-RemLawrence/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20210208141154.png)

      - c) ![](https://latex.codecogs.com/svg.latex?\Large&space;\vec{a}\times\vec{b})
![alt text](https://github.com/CS-2053-Winter-2021/concept-assignment-2-RemLawrence/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20210208142503.png)

      - d) ![](https://latex.codecogs.com/svg.latex?\Large&space;\vec{a}\cdot\vec{b})
![alt text](https://github.com/CS-2053-Winter-2021/concept-assignment-2-RemLawrence/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20210208142908.png)


 7. Create a world transform matrix that translates by 
      
      ![](https://latex.codecogs.com/svg.latex?\Large&space;\langle3,4,2\rangle)
      
      and rotates it 90° about the x-axis.
![alt text](https://github.com/CS-2053-Winter-2021/concept-assignment-2-RemLawrence/blob/master/QQ%E6%B5%8F%E8%A7%88%E5%99%A8%E6%88%AA%E5%9B%BE20210209151230.png)
