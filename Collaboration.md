# Collaboration Module
CollaborationManager provides the following functions:
  - Group devices by rooms to let them collaborate with each other.
  - Let a wide range of devices communicate through the Workstation.
  - Wrap generic message format and communicatio channels to make
    collaborations easier. 
    
## Add Collaboration module
In order to make things work, be sure to be familiar with METoolKit
and previous steps of this tutorials were followed.

- In Unity, open **Assets->Streming Assets**.
  Search for **MEConfigNetwork.ini** and open it.
<p align="left">
<img src="https://github.com/angelicaCruz/Tutorial/blob/master/collaboration1.png">
</p>

- Make sure that it contains the value provided below. 
```
##############################################
# config for network
###############################################

Server_Host = 192.168.2.31
Server_Port = 8848
```
- It is possible to use personal server IP.
  **Note:**
    - If application is not running on Unity Editor or PC Standalone(Hololens,iOS,Android),
      app will load **config file** at **PersistentDataPath** and not on Streaming Assets.
      For more information, please refer to [Utility: Config Files](http://docs.datamesh.com/projects/me-live/en/latest/toolkit/toolkit-man-utility-config-file/)
    - Having the wrong host IP address will cause the application to log a **Delay=0**.
      Notice the difference between the two pictures below.
<p align="left">
<img src="https://github.com/angelicaCruz/Tutorial/blob/master/collaboration2.png">
<img src="https://github.com/angelicaCruz/Tutorial/blob/master/collaboration3.png">
</p>
    - If server address is right, you will also see:
      ```
      Enter Room Sucessfully
      UnityEngine.Debug:Log(Object)
      ```

- Open the MyAppScript. Find COLLABORATION section and add pieces of code as below.
  ```c#
  using System.Collections;
  using UnityEngine;
  using DataMesh.AR;
  using DataMesh.AR.Network;
  using MEHoloClient.Entities;
  using MEHoloClient.Proto;
  using DataMesh.AR.Interactive;
  using DataMesh.AR.Anchor;

  public class MainApp : MonoBehaviour
  {

      public GameObject cube;
      private MultiInputManager inputManager;
      //COLLABORATION
      CollaborationManager cm;
      private ShowObject showObject;
      private SceneObject roomData;
      //END OF COLLABORATION


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
          //section 1: INPUT section
          inputManager = MultiInputManager.Instance;
          inputManager.cbTap += OnTap;

          //COLLABORATION
          cm = CollaborationManager.Instance;
          cm.cbEnterRoom = cbEnterRoom;
          cm.TurnOn();

          string showId = "showId001";
          string obj_type = "ColorType";

          MsgEntry msg = new MsgEntry();
          msg.ShowId = showId;

          ObjectInfo info = new ObjectInfo();
          info.ObjType = obj_type;
          msg.Info = info;

          showObject = new ShowObject(msg);
          roomData = new SceneObject();
          roomData.ShowObjectDic.Add(showObject.ShowId, showObject);

          cm.roomInitData = roomData;
          cm.TurnOn();
          //END OF COLLABORATION
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
                  break;

              //section2: ANCHOR section
              /*case 3:
                  sum--;
                  SceneAnchorController.Instance.AddCallbackFinish(ModifyAnchorFinish);
                  SceneAnchorController.Instance.TurnOn();
                  break;*/

              //COLLABORATION
              case 3:
                  cube.GetComponent<MeshRenderer>().material.color = Color.red;
                  cube.transform.Rotate(new Vector3(0,30,0));
                  break;

              case 4:
                  cube.GetComponent<MeshRenderer>().material.color = Color.blue;
                  cube.transform.rotation = new Quaternion(0, 0, 0, 0);
                  break;
              //END OF COLLABORATION
          }
      }

      private void ModifyAnchorFinish()
      {
          SceneAnchorController.Instance.RemoveCallbackFinish(ModifyAnchorFinish);
          SceneAnchorController.Instance.TurnOff();
          sum = 2;
      }

      //COLLABORATION
      private void cbEnterRoom()
      {
          Debug.Log("Enter Room Sucessfully");
      }
  }
  ```
- Save the modified script.
- Build project and deploy pn Hololens.
