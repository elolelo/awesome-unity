# Code Basics
<details>
  <summary>Player Movement</summary>

  ```csharp
  using UnityEngine;
  using System.Collections;

  public class PlayerController : MonoBehaviour {

      public float speed;

      private Rigidbody rb;

      void Start ()
      {
          rb = GetComponent<Rigidbody>();
      }

      void FixedUpdate ()
      {
          float moveHorizontal = Input.GetAxis ("Horizontal");
          float moveVertical = Input.GetAxis ("Vertical");

          Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);

          rb.AddForce (movement * speed);
      }
  }
  ```
</details>
<details>
  <summary>Moving Camera</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class CameraController : MonoBehaviour {

    public GameObject player;

    private Vector3 offset;

    void Start ()
    {
        offset = transform.position - player.transform.position;
    }

    void LateUpdate ()
    {
        transform.position = player.transform.position + offset;
    }
}
  ```
</details>
<details>
  <summary>Collectable Objects</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class PlayerController : MonoBehaviour {

    void OnTriggerEnter(Collider other) 
    {
        if (other.gameObject.CompareTag ("Pick Up"))
        {
            other.gameObject.SetActive (false);
        }
    }
}
  ```
</details>
<details>
  <summary>Score Display</summary>

  ```csharp
using UnityEngine;
using UnityEngine.UI;
using System.Collections;

public class PlayerController : MonoBehaviour {

    public Text countText;
    public Text winText;
    private int count;

    void Start ()
    {
        count = 0;
        SetCountText();
        winText.text = "";
    }

    void OnTriggerEnter(Collider other) 
    {
        if (other.gameObject.CompareTag ( "Pick Up"))
        {
            count = count + 1;
            SetCountText ();
        }
    }

    void SetCountText ()
    {
        countText.text = "Count: " + count.ToString ();
        if (count >= 12)
        {
            winText.text = "You Win!";
        }
    }
}
  ```
</details>
<details>
  <summary>Behaviour Components</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class ExampleBehaviourScript : MonoBehaviour
{
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.R))
        {
            GetComponent<Renderer> ().material.color = Color.red;
        }
    }
}
  ```
</details>
<details>
  <summary>Check State</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class CheckState : MonoBehaviour
{
    public GameObject myObject;

    void Start ()
    {
        Debug.Log("Active Self: " + myObject.activeSelf);
        Debug.Log("Active in Hierarchy" + myObject.activeInHierarchy);
    }
}
  ```
</details>
<details>
  <summary>Translate and Rotate</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class TransformFunctions : MonoBehaviour
{
    public float moveSpeed = 10f;
    public float turnSpeed = 50f;

    void Update ()
    {
        if(Input.GetKey(KeyCode.UpArrow))
            transform.Translate(Vector3.forward * moveSpeed * Time.deltaTime);

        if(Input.GetKey(KeyCode.DownArrow))
            transform.Translate(-Vector3.forward * moveSpeed * Time.deltaTime);

        if(Input.GetKey(KeyCode.LeftArrow))
            transform.Rotate(Vector3.up, -turnSpeed * Time.deltaTime);

        if(Input.GetKey(KeyCode.RightArrow))
            transform.Rotate(Vector3.up, turnSpeed * Time.deltaTime);
    }
}
  ```
</details>
<details>
  <summary>Look At</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class CameraLookAt : MonoBehaviour
{
    public Transform target;

    void Update ()
    {
        transform.LookAt(target);
    }
}
  ```
</details>
<details>
  <summary>Linear Interpolation</summary>

  ```csharp
// In this case, result = 4
float result = Mathf.Lerp (3f, 5f, 0.5f);
// The Mathf.Lerp function takes 3 float parameters: one representing the value to interpolate from; another representing the value to interpolate to and a final float representing how far to interpolate

Vector3 from = new Vector3 (1f, 2f, 3f);
Vector3 to = new Vector3 (5f, 6f, 7f);

// Here result = (4, 5, 6)
Vector3 result = Vector3.Lerp (from, to, 0.75f);

// The same principle is applied when using Color.Lerp.
// In the Color struct, colours are represented by 4 floats representing red, blue, green and alpha.
// When using Lerp, these floats are interpolated just as with Mathf.Lerp and Vector3.Lerp.

void Update ()
{
    light.intensity = Mathf.Lerp(light.intensity, 8f, 0.5f * Time.deltaTime);
    // With deltaTime, the change to intensity would happen per second instead of per frame.
}
  ```
</details>
<details>
  <summary>GetAxis Horizontal and Vertical</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class DualAxisExample : MonoBehaviour 
{
    public float range;
    public GUIText textOutput;

    void Update () 
    {
        float h = Input.GetAxis("Horizontal");
        float v = Input.GetAxis("Vertical");
        float xPos = h * range;
        float yPos = v * range;

        transform.position = new Vector3(xPos, yPos, 0);
        textOutput.text = "Horizontal Value Returned: "+h.ToString("F2")+"\nVertical Value Returned: "+v.ToString("F2");    
    }
}
  ```
</details>
<details>
  <summary>OnMouseDown</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class MouseClick : MonoBehaviour
{
    void OnMouseDown ()
    {
        rigidbody.AddForce(-transform.forward * 500f);
        rigidbody.useGravity = true;
    }
}
  ```
</details>
<details>
  <summary>Using Other Components</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class UsingOtherComponents : MonoBehaviour
{
    public GameObject otherGameObject;

    private AnotherScript anotherScript;
    private YetAnotherScript yetAnotherScript;
    private BoxCollider boxCol;

    void Awake ()
    {
        anotherScript = GetComponent<AnotherScript>();
        yetAnotherScript = otherGameObject.GetComponent<YetAnotherScript>();
        boxCol = otherGameObject.GetComponent<BoxCollider>();
    }

    void Start ()
    {
        boxCol.size = new Vector3(3,3,3);
        Debug.Log("The player's score is " + anotherScript.playerScore);
        Debug.Log("The player has died " + yetAnotherScript.numberOfPlayerDeaths + " times");
    }
}
  ```
</details>
<details>
  <summary>Using Delta Times</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class UsingDeltaTime : MonoBehaviour
{
    public float speed = 8f; 
    public float countdown = 3.0f;

    void Update ()
    {
        countdown -= Time.deltaTime;
        if(countdown <= 0.0f)
            light.enabled = true;

         if(Input.GetKey(KeyCode.RightArrow))
            transform.position += new Vector3(speed * Time.deltaTime, 0.0f, 0.0f);
    }   
}
  ```
</details>
<details>
  <summary>Using Data Types</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class DatatypeScript : MonoBehaviour 
{
    void Start () 
    {
        //Value type variable
        Vector3 pos = transform.position;
        pos = new Vector3(0, 2, 0);

        //Reference type variable
        Transform tran = transform;
        tran.position = new Vector3(0, 2, 0);
    }
}
  ```
</details>
<details>
  <summary>Using Instantiate</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class UsingInstantiate : MonoBehaviour
{
    public Rigidbody rocketPrefab;
    public Transform barrelEnd;


    void Update ()
    {
        if(Input.GetButtonDown("Fire1"))
        {
            Rigidbody rocketInstance = Instantiate(rocketPrefab, barrelEnd.position, barrelEnd.rotation) as Rigidbody;
            rocketInstance.AddForce(barrelEnd.forward * 5000);
        }
    }
}
  ```
</details>
<details>
  <summary>Arrays</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class Arrays : MonoBehaviour
{
    public GameObject[] players;

    void Start ()
    {
        players = GameObject.FindGameObjectsWithTag("Player");

        for(int i = 0; i < players.Length; i++)
        {
            Debug.Log("Player Number "+i+" is named "+players[i].name);
        }
    }
}
  ```
</details>
<details>
  <summary>Invoke</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class InvokeScript : MonoBehaviour 
{
    public GameObject target;

    void Start()
    {
        Invoke (nameof(SpawnObject), 2);
        // Repeating
        InvokeRepeating(nameof(SpawnObject), 2, 1);
        // TODO: Use UniRx/Observables instead :)
    }

    void SpawnObject()
    {
        float x = Random.Range(-2.0f, 2.0f);
        float z = Random.Range(-2.0f, 2.0f);
        Instantiate(target, new Vector3(x, 2, z), Quaternion.identity);
    }
}
  ```
</details>
<details>
  <summary>Enumerations</summary>

  ```csharp
using UnityEngine;
using System.Collections;

public class EnumScript : MonoBehaviour 
{
    enum Direction {North, East, South, West};

        void Start () 
    {
        Direction myDirection;

        myDirection = Direction.North;
    }

    Direction ReverseDirection (Direction dir)
    {
        if(dir == Direction.North)
            dir = Direction.South;
        else if(dir == Direction.South)
            dir = Direction.North;
        else if(dir == Direction.East)
            dir = Direction.West;
        else if(dir == Direction.West)
            dir = Direction.East;

        return dir;     
    }
}
  ```
</details>