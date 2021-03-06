---
layout: post
title: "VR - Scripting in Unity"
description: "C# Snippet Compilation of Unity scripting basics"
date: 2016-11-30
tags: [design, code]
comments: true
share: true
---

## Scripting Basics Snippets Guide in 'C#' ##

> **01. Scripts as Behaviours Components**

```c#
using UnityEngine;
using System.Collections;

public class ExampleBehaviourScript : MonoBehaviour
{
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.R))
        {
            GetComponent<Renderer>().material.color = Color.red;
        }
        if (Input.GetKeyDown(KeyCode.G))
        {
            GetComponent<Renderer>().material.color = Color.green;
        }
        if (Input.GetKeyDown(KeyCode.B))
        {
            GetComponent<Renderer>().material.color = Color.blue;
        }
    }
}
```
> **02. Variables and Functions**

```c#
using UnityEngine;
using System.Collections;

public class VariablesAndFunctions : MonoBehaviour
{
    int myInt = 5;

    void Start()
    {
       myInt = MultiplyByTwo(myInt);
       print(myInt);
    }

    int MultiplyByTwo(int number)
    {
        int res;
        res = number * 2;
        return res;
    }
}
```

> **03. Conventions and Syntax**

```c#
using UnityEngine;
using System.Collections;

public class ConventionsAndSyntax : MonoBehaviour
{
    void Start()
    {
        print(transform.position.x);

        if (transform.position.y <= 5f)
        {
            print("I'm about to hit the ground!");
        }
    }
}
```

> **04. IF Statements**

```c#
using UnityEngine;
using System.Collections;

public class IfStatements : MonoBehaviour
{
    float coffeTemperature = 85.0 f;
    float hotLimitTemperature = 70.0 f;
    float coldLimitTemperature = 40.0 f;

    void Update()
    {
        if(Input.GetKeyDown(KeyCode.Space))
            TemperatureTest();

        coffeTemperature -= Time.deltaTime * 5f;
    }

    TemperatureTest()
    {
        if(coffeTemperature > hotLimitTemperature)
        {
            print("Coffee is too hot!");
        }
         if(coffeTemperature < coldLimitTemperature)
        {
            print("Coffee is too cold");
        }
         else
        {
            print("just right!");
        }
    }
}
```

> **05a. For Loop**

```c#
using UnityEngine;
using System.Collections;

public class ForLoop : MonoBehaviour
{
    int numEntities = 3;

    void Start()
    {
        for (int i=0; i<numEntities; i++)
        {
            print("Creating number: " + i);
        }
    }
}
```

> **05b. While Loop**

```c#
using UnityEngine;
using System.Collections;

public class While : MonoBehaviour
{
    int cupInTheSink = 4;

    void Start()
    {
        while(cupInTheSink > 0) 
        {
            print("I've washed a cup!");
            cupInTheSink--;
        }
    }
}
```

> **05c. DoWhile Loop**

```c#
using UnityEngine;
using System.Collections;

public class DoWhile : MonoBehaviour // it will execute only the first time
{
    void Start()
    {
        bool shouldContinue = false;

        do{
            print("Hello World!");
        }
        while( shouldContinue == true);
    }
}
```

> **05d. ForEach Loop**

```c#
using UnityEngine;
using System.Collections;

public class Foreach : MonoBehaviour // Foreach in
{
    void Start()
    {
        string[] strings = new string[3];

        string[0] = "First string";
        string[1] = "Second string";
        string[2] = "Third string";

        Foreach(string item in string)
        {
            print("item");
        }
    }
}
```

> **06. ScopeAndAccessModifiers**

```c#
using UnityEngine;
using System.Collections;

public class ScopeAndAccessModifiers : MonoBehaviour 
{
    public int alpha = 5;

    private int beta = 0;
    private int gamma = 5;

    private AnotherClass myOtherClass();

    void Start ()
    {
        alpha = 29;

        myOtherClass = new AnotherClass();
        myOtherClass.FruitMachine(alpha, myOtherClass.apples);
    }

    void Example (int pens, int crayons)
    {
        int answer;
        answer = pens * crayons * alpha;
        print(answer);
    }

    void Update()
    {
        print("Alpha is set to: " + alpha);
    }
}

// AnotherClass

using UnityEngine;
using System.Collections;

public class AnotherClass
{
    public int apples;
    public int bananas;
    
    
    private int stapler;
    private int sellotape;
    
    
    public void FruitMachine (int a, int b)
    {
        int answer;
        answer = a + b;
        Debug.Log("Fruit total: " + answer);
    }
    
    
    private void OfficeSort (int a, int b)
    {
        int answer;
        answer = a + b;
        Debug.Log("Office Supplies total: " + answer);
    }
}
```

> **07. AwakeAndStart**

```c#
using UnityEngine;
using System.Collections;

public class AwakeAndStart : MonoBehaviour
{
    void Awake()
    {
        print("Awake called");
    }
    
    void Start()
    {
        Debug.Log("Start called");
    }
}
```

> **08. UpdateAndFixedUpdate**

```c#
using UnityEngine;
using System.Collections;

public class UpdateAndFixedUpdate : MonoBehaviour
{
    void FixedUpdate() // Called every pshysics Step
    {
        Debug.Log("FixedUpdate time: + Time.deltaTime");
    }

    void Update() // Called update frame
    {
        Debug.Log("Update time: + Time.deltaTime");
    }
}
```

> **09.a Vector3.Angle**

```c#
using UnityEngine;
public class AngleExample : MonoBehaviour
{
	public Transform     target;

	// prints "close" if the z-axis of this transform looks
	// almost towards the target

	void Update ()
	{
		Vector3 targetDir = target.position - transform.position;
		float angle = Vector3.Angle( targetDir, transform.forward );

		if( angle < 5.0f )
			print( "close" );
	}
}
```

> **09.b Vector3.Cross**

```c#
using UnityEngine;
using System.Collections;

public class ExampleClass : MonoBehaviour 
{
    Vector3 GetNormal(Vector3 a, Vector3 b, Vector3 c) {
        Vector3 side1 = b - a;
        Vector3 side2 = c - a;
        return Vector3.Cross(side1, side2).normalized;
    }
}
```

> **09.c Vector3.Distance**

```c#
using UnityEngine;
using System.Collections;

public class ExampleClass : MonoBehaviour 
{
    public Transform other;
    void Example() {
        if (other) {
            float dist = Vector3.Distance(other.position, transform.position);
            print("Distance to other: " + dist);
        }
    }
}
```

> **09.d Vector3.Lerp**

```c#
using UnityEngine;
using System.Collections;

public class ExampleClass : MonoBehaviour 
{
    public Transform startMarker;
    public Transform endMarker;
    public float speed = 1.0F;
    private float startTime;
    private float journeyLength;
    void Start() {
        startTime = Time.time;
        journeyLength = Vector3.Distance(startMarker.position, endMarker.position);
    }
    void Update() {
        float distCovered = (Time.time - startTime) * speed;
        float fracJourney = distCovered / journeyLength;
        transform.position = Vector3.Lerp(startMarker.position, endMarker.position, fracJourney);
    }
}
```

> **10 EnableComponents**

```c#
using UnityEngine;
using System.Collections;

public class EnableComponents : MonoBehaviour 
{
    private Light myLight;

    void Start()
    {
        myLight = GetComponent<Light>;
    }

    void Update()
    {
        if(Input.GetKeyDown(KeyCode.Space))
        {
            myLight.enabled = !myLight.enabled; // switch
        }
    }
}
```

> **11. ActiveObjects**

```c#
using UnityEngine;
using System.Collections;

public class ActiveObjects : MonoBehaviour 
{
    void Start()
    {
        gameObject.SetActive(false);
    }
}

using UnityEngine;
using System.Collections;

public class CheckState : MonoBehaviour 
{
    public GameObject myObject;
    
    void Start()
    {
        Debug.Log("Active Self: " + myObject.activeSelf);
        Debug.Log("Active in Hierarchy" + myObject.activeInHierarchy);
    }
}
```
> **12. TransformFunctions**

```c#
using UnityEngine;
using System.Collections;

public class TransformFunctions : MonoBehaviour 
{
    public float moveSpeed = 10f;
    public float turnSpeed = 50f;

    void Update()
    {
        if(Input.GetKey(KeyCode.UpArrow))
            transform.Translate(Vector3.forward * moveSpeed * Time.deltaTime);

        if(Input.GetKey(KeyCode.DownArrow))
            transform.Translate(Vector3.down * moveSpeed * Time.deltaTime);

        if(Input.GetKey(KeyCode.LeftArrow))
            transform.Rotate(Vector3.up * turnSpeed * Time.deltaTime);

        if(Input.GetKey(KeyCode.RightArrow))
            transform.Rotate(Vector3.up * turnSpeed * Time.deltaTime);      
    }
}
```
> **13. CameraLookAt**

```c#
using UnityEngine;
using System.Collections;

public class CameraLookAt : MonoBehaviour 
{
    public Transform target;

    void Uppdate()
    {
        transform.LookAt(target);
    }
}
```
> **14. LinearInterpolation**

```c#
using UnityEngine;
using System.Collections;

public class LinearInterpolation : MonoBehaviour 
{
    void Uppdate()
    {
        // interpolate between 3 and 5 for 50%
        float result = Mathf.Lerp(3f, 5f, 0.5f);

        Vector3 from = new Vector3(1f, 2f, 3f);
        Vector3 to = new Vector3(5f, 6f, 7f);
    }

    void Uppdate()
    {
        Vector3 from = new Vector3(1f, 2f, 3f);
        Vector3 to = new Vector3(5f, 6f, 7f);

        //Here the result = (4,5,6) > the 75% between points
        Vector3 result = Vector3.Lerp(from, to, 0.75f);
    }

        void Uppdate()
    {
        // from 0f tp 8f by 0.5f - frame depenent ( every frame goes 0.5 closer)
        light.intensity = Mathf.Lerp(light.intesity, 8f, 0.5f);
    }

     void Uppdate()
    {
        // from 0f tp 8f by 0.5f - frame indepenent ( every second goes 0.5 closer)
        light.intensity = Mathf.Lerp(light.intesity, 8f, 0.5f * Time.deltaTime);
    }
```

> **15. Destroy**

```c#
using UnityEngine;
using System.Collections;

public class DestroyBasic : MonoBehaviour 
{
    void Update()
    {
        if(Input.GetKey(KeyCode.Space))
        {
            Destroy(gameObject);
        }
    }
}

public class DestroyOther : MonoBehaviour 
{
    void Update()
    {
        if(Input.GetKey(KeyCode.Space))
        {
            Destroy(other);
        }
    }
}

public class DestroyComponent : MonoBehaviour 
{
    void Update()
    {
        if(Input.GetKey(KeyCode.Space))
        {
            Destroy(GetComponent<MeshRenderer>());
        }
    }
}
```

> **16. KeyInput**

```c#
using UnityEngine;
using System.Collections;

public class KeyInput : MonoBehaviour 
{
    public GUITexture graphic;
    public Texture2D standard;
    public Texture2D downgfx;
    public Texture2D upgfx;
    public Texture2D heldgfx;

    void Start()
    {
            graphic.texture = standard;
    }

    void Update()
    {
        bool down = Input.GetKeyDown(KeyCode.Space);
        bool held = Input.GetKey(KeyCode.Space);
        bool up = Input.GetKeyUp(KeyCode.Space);

        if(down)
        {
            graphic.texture = downgfx;
        }
        else if(held)
        {
            graphic.texture = heldgfx
        }
        else if(up)
        {
            graphic.texture = upgfx
        }
        else
        {
            green.texture = standard
        }

        guiText.text = " " + down + "\n" + up;
    }
}


// BUTTON INPUT

public class ButtonInput : MonoBehaviour
{
    public GUITexture graphic;
    public Texture2D standard;
    public Texture2D downgfx;
    public Texture2D upgfx;
    public Texture2D heldgfx;
    
    void Start()
    {
        graphic.texture = standard;
    }
    
    void Update ()
    {
        bool down = Input.GetButtonDown("Jump");
        bool held = Input.GetButton("Jump");
        bool up = Input.GetButtonUp("Jump");
        
        if(down)
        {
            graphic.texture = downgfx;
        }
        else if(held)
        {
            graphic.texture = heldgfx;
        }
        else if(up)
        {
            graphic.texture = upgfx;
        }
        else
        {
            graphic.texture = standard;
        }
    
        guiText.text = " " + down + "\n " + held + "\n " + up;
    }
}
```

> **17. GetAxis** // mainly dor joysticks

```ruby
using UnityEngine;
using System.Collections;

public class AxisSimple : MonoBehaviour
{
    public float range;
    public guiText textOutput;

    void Update()
    {
        float h = Input.GetAxis("Horizontal");
        float xPos = h * range;

        transform.position = new Vector3 (xPos, 2f, 0);
        textOutput.text = "Value Returned: " + h.ToString("F2");
    }
}

using UnityEngine;
using System.Collections;

public class AxisRawExample : MonoBehaviour
{
    public float range;
    public guiText textOutput;

    void Update()
    {
        float h = Input.GetRaw("Horizontal");
        float xPos = h * range;

        transform.position = new Vector3 (xPos, 2f, 0);
        textOutput.text = "Value Returned: " + h.ToString("F2");
    }
}

using UnityEngine;
using System.Collections;

public class DualAxisExample : MonoBehaviour
{
    public float range;
    public guiText textOutput;

    void Update()
    {
        float h = Input.GetRaw("Horizontal");
        float v = Input.GetRaw("Vertical");
        float xPos = h * range;
        float yPos = v * range;

        transform.position = new Vector3 (xPos, 2f, 0);
        textOutput.text = "Horizontal Value Returned: " + h.ToString("F2") + +"\nVertical Value Returned: "+v.ToString("F2");
    }
}
```
> **18. UsingOtherComponents**

```ruby
using UnityEngine;
using System.Collections;

public class UsingOtherComponents : MonoBehaviour
{
    public GameObject otherGameObject;

    private AnotherScript anotherScript;
    private YetAnotherScript yetAnotherScript;
    private BoxCollider boxCol;

    void Awake()
    {
        anotherScript = GetComponent<AnotherScript>();
        yetAnotherScript = otherGameObject.GetComponent<YetAnotherScript>();
        boxCol = otherGameObject.GetComponent<BoxCollider>();
    }

    void Start()
    {
        boxCol.size = new Vector3(3,3,3);
        Debug.Log("The Player's score is" + anotherScript.playerScore);
        Debug.Log("The player is alive" + yetAnotherScript.numberOfPlayersAlive + "times");
    }
}

public class AnotherScript : MonoBehaviour
{
    public int playerSocre = 9001;
}

public class YetAnotherScript : MonoBehaviour
{
    publuc int numberOfPlayersAlive = 3;
}
```
> **19. UsingDeltaTime**

```c#
using UnityEngine;
using System.Collections;

public class UsingDeltaTime : MonoBehaviour
{
    public float speed = 8f;
    public float countdown = 3.0f

    void Update()
    {
        countdown -= Time.deltaTime;
        if (countdown <= 0.0f)
            light.enabled = true;
        
        if (Input.GetKey(KeyCode.RightArrow))
            transform.position += new Vector3(speed * Time.deltaTime, 0.0f, 0.0f);
    }
}
```

> **20. DatatypeScript**

```c#
using UnityEngine;
using System.Collections;

public class DatatypeScript : MonoBehaviour
{
 void Start()
    {
        // value type Variables > Struct (combined value type)
        Vector3 pos = transform.position; // we are making a COPY
        pos = new Vector3(0,2,0); // wont' move unless assigning it back

        //Reference type variable;
        Transform tran = transform;// we are making a REFERENCED COPY
        tran.position = new Vector3(0,2,0);// so when we change the variable we change the original
    }
}
```

> **21. HowClassesWork**

```c#
using UnityEngine;
using System.Collections;

public class HowClassesWork : MonoBehaviour
{
    public class Stuff
    {
        public int bullets;
        public int grenades;
        public int rockets;

        public Stuff (int bul, int gre, int roc)
        {
            bullets = bul;
            grenades = gre;
            rockets = roc;
        }
    }

    public Stuff myStuff = new Stuff(10, 7, 25);
    public float speed;
    public float turnSpeed;
    public Rigidbody bulletPrefab;
    public Transform firePosition;
    public float bulletSpeed;

    void Update()
    {
        Movement();
        Shoot();
    }

    void Movement()
    {
        float forwardMovement = Input.GetAxis("Vertical") * speed * Time.deltaTime;
        float turnMovement  Input.GetAxis("Horizontal") * turnSpeed * Time.deltaTime;

        transform.Translate(Vector3.forward * forwardMovement);
        transform.Rotate(Vector3.up * turnMovement);
    }

    void Shoot()
    {
        if (Input.GetButtonDown("Fire1") && myStuff.bullets > 0)
        {
            Rigidbody bulletInstance = Instantiate(bulletPrefab, firePosition.position, firePosition.rotation) as Rigidbody;
            bulletInstance.AddForce(firePosition.forward * bulletSpeed);
            myStuff.bullets--;
        }
    }
}

// Here we do the same HowClassesWork but in 3 different scripts
public class Inventory : MonoBehaviour
{
    public class Stuff
    {
        public int bullets;
        public int grenades;
        public int rockets;
        public float fuel;

         // Constructor 1
        public Stuff()
        {
            bullets = 1;
            grenades = 1;
            rockets = 1;
        }
        // Constructor 2
        public Stuff(int bul, int, gre, int roc);
        {
            bullets = bul;
            grenades = gre;
            rockets = roc;
        }
        // Constructor 3
        public Stuff(int bul, float fu)
        {
            bullets = bul;
            fuel = fu;
        }
    }

    // Creating an Instance (an Object) of the Stuff class
    public Stuff myStuff = new Stuff(50, 5, 5);

    public Stuff myOtherStuff = new Stuff(50, 1.5f);

    void Start()
    {
        Debug.Log(myStuff.bullets);
    }
}

using UnityEngine;
using System.Collections;

public class MovementControls : MonoBehaviour
{
    public float speed;
    public float turnSpeed;

    void Update()
    {
        Movement();
    }

    voidMovement()
    {
        float forwardMovement = Input.GetAxis("Vertical")*speed*Time.deltaTime;
        float turnMovement = Input.GetAxis("Horizontal")*turnSpeed*time.deltaTime;

        transform.Translate(Vector3.forward*forwardMovement);
        transform.Rotate(Vector3.up*turnMovement);
    }
}

using UnityEngine;
using System.Collections;

public class Loving : MonoBehaviour
{
    public Rigidbody bulletPrefab;
    public Transform firePosition;
    public float bulletSpeed;

    private Inventory inventory;

    void Awake()
    {
        inventory = GetComponent<Inventory>();
    }

    void Update()
    {
        Shoot();
    }

    void Shoot()
    {
        if(Input.GetButtonDown("Fire1")&& inventory.myStuff.bullets > 0)
        {
            Rigidbody bulletInstance = Instantiate(bulletPrefab, firePosition.position, firePosition.rotation)as Rigidbody;
            bulletInstance.AddForce(firePosition.position * bulletSpeed);
            inventory.myStuff.bullets--;
        }
    }
}
```
> **22. Instantitaion**

```c#
using UnityEngine;
using System.Collections;

public class Instantitaion : MonoBehaviour
{
    public Rigidbody rocketPrefab;
    public Transform barrelEnd;
    public float speed;

    void Update()
    {
        if(Input.GetButtonDown("Fire1"))
        {
            Rigidbody rocketInstance;
            rocketInstance = Instantiate(rocketPrefab, barrelEnd.transform, barrelEnd.rotation);
            rocketInstance.AddForce(barrelEnd.forward * speed);
        }
    }
}

using UnityEngine;
using System.Collections;

public class RocketsDestruction : MonoBehaviour
{
    void Start()
    {
        Destroy(gameObject, 1.5f);//after 1.5 seconds
    }
}
```

> **23. Arrays**

```C#
using UnityEngine;
using System.Collections;

public class Arrays : MonoBehaviour
{
    public GameObject[] players;

    void Start()
    {
        players = GameObject.FindGameObjectsWithTag("player");

        for (i=0; i<players.Length; i++)
        {
            Debug.Log("Player Number" +i+" is named" + players[i].name);            
        }
    }
}
```

> **24. Invoke**

```C#
using UnityEngine;
using System.Collections;

public class Invoke : MonoBehaviour
{
    public GameObject target;

    void Start()
    {
        Invoke("SpawnObject", 2); // 2 sec delay
    }

    void SpawnObject()
    {
        Instantiate(target, new Vector3(0, 2, 0), Quaternion.identity);
        // You can only invoke void Functions
    }
}

public class InvokeRepeating : MonoBehaviour
{
    public GameObject target;

    void Start()
    {
        InovkeRepeat("SpawnObject", 2, 1);
        // delay in sec after first spawn, and between them
    }

    void SpawnObject()
    {
        float x = Random.Range(-2.0f, 2.0f);
        float z = Random.Range(-2.0f, 2.0f);
        Instantiate(target, new Vector3(x, 2, z), Quaternion.identity);
    }
}
```
> **25. Enumerations**

```C#
using UnityEngine;
using System.Collections;

public class Enumscript : MonoBehaviour
{
    enum Direction {North, East, South, West};

    void Start()
    {
        Direction myDirection;
        myDirection = Direction.North;
    }

    Direction ReverseDirection (Direction dir)
    {
        if(dir==Direction.North)
            dir = Direction.South;
        else if(dir==Direction.South)
            dir = Direction.North;
        else if(dir==Direction.East)
            dir = Directio.West;
        else if(dir==)Direction.West)
            dir = Direction.East;
        
        return dir;
    }
}
```
> **26. Switch**

```C#
using UnityEngine;
using System.Collections;

public class Switch : MonoBehaviour
{
    public int intelligence = 5;

    void Greet()
    {
        switch(intelligence)
        {
            case 5:
                print("Super Intelligent");
                break;
            case 4:
                print("Very Intelligent");
                break;
            case 3:
                print("Intelligent");
                break;
            case 2:
                print("Not so much");
                break;
            case 1:
                print("mmmhhh");
                break;
            default:
                print("Incorrect Intelligence level");
                break;
        }
    }
}
```
> **End of Scripts as Behaviours Components**
