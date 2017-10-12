# First App
After following the previous steps, we can now make a simple Hololens application
using both Unity and METoolKit. 

## Input
- Place a cube where camera can capture.
- Select MainApp gameobject in the Heirarchy and open the MainAppScript component.
  Copy and paste the following code.
  ```c#
  using System.Collections;
  using UnityEngine;
  using DataMesh.AR;
  using DataMesh.AR.Network;
  using MEHoloClient.Entities;
  using MEHoloClient.Proto;
  using DataMesh.AR.Interactive;

  public class MainApp : MonoBehaviour
  {
      public GameObject cube;
      private MultiInputManager inputManager;
      private int sum;

      void Start()
      {
          StartCoroutine(WaitForInit());
          //initialize sum to 0
          sum = 0;
      }

      private IEnumerator WaitForInit()
      {
          MEHoloEntrance entrance = MEHoloEntrance.Instance;
          while (!entrance.HasInit)
          {
              yield return null;
          }

          // Todo: Initialize modules and variable
          //INPUT section
          inputManager = MultiInputManager.Instance;
          inputManager.cbTap += OnTap;
      }

      //create OnTap()
      private void OnTap(int count)
      {
          sum += count;
          switch (sum)
          {
              case 1:
                  //cube changes color to red
                  cube.GetComponent<MeshRenderer>().material.color = Color.red;
                  break;

              case 2:
                  //cube turns blue
                  cube.GetComponent<MeshRenderer>().material.color = Color.blue;
          }
      }
  }
  ```  
 <p align="left">
 <img src="https://github.com/angelicaCruz/Tutorial/blob/master/input.png">
 </p>
  
  - Save code. Go to Unity and drag the Cube into MainAppScript component.
  - Press **Play** and see what happens.
  - To simulate Air Tap, press **Enter** on the keyboard.
  - Get a Hololens device, build the project in Unity and deploy. 
  
  After deploying the application on device, notice that there is already a cursor.
  When Gaze is directed into a gameobject, the cursor is a hand while it is only a dot
  when there is no detected object in Gaze direction.
