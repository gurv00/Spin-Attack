//# Spin-Attack
//The player can use an attack where they spin their weapon in a circle (Zelda Spin Attack)
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour {

    private Animator anim;
    private Rigidbody2D myRigidbody;

    public float spinAttackTime;
    private float spinAttackTimeCounter;
         
         void Start () {

        anim = GetComponent<Animator>();
        myRigidbody = GetComponent<Rigidbody2D>();
        }
         
         void Update () {
         if (Input.GetAxisRaw("Horizontal") > 0.5f || Input.GetAxisRaw("Horizontal") < -0.5f)
            {
                
                myRigidbody.velocity = new Vector2(Input.GetAxisRaw("Horizontal") * currentMoveSpeed, myRigidbody.velocity.y);
                playerMoving = true;
                lastMove = new Vector2(Input.GetAxisRaw("Horizontal"), 0f);
            }

            if (Input.GetAxisRaw("Vertical") > 0.5f || Input.GetAxisRaw("Vertical") < -0.5f)
            {
                
                myRigidbody.velocity = new Vector2(myRigidbody.velocity.x, Input.GetAxisRaw("Vertical") * currentMoveSpeed);
                playerMoving = true;
                lastMove = new Vector2(0f, Input.GetAxisRaw("Vertical"));
            }
         //Collects the input from the player
         if (Input.GetKey(KeyCode.K))
            {
            //spinAttackTime can be set in unity or in script, used to determine how long the Counter should run
                spinAttackTimeCounter = spinAttackTime;
                //Tells the animator in Unity to execut the spin attack animation
                anim.SetBool("SpinAttack", true);

            }
            
        //checks if the spiAttackTime is greater than 0, which was set by the spinAttackTime variable
        if (spinAttackTimeCounter > 0)
        {
        //Decrements the time that was set by the spinAttackTime variable
            spinAttackTimeCounter -= Time.deltaTime;
        }
        
        //checks if the spinAttackTime is less than 0 which would signify that the attack should stop playing
        if (spinAttackTimeCounter <= 0)
        {
        //tells the animator to stop playing the spinattack animation
            anim.SetBool("SpinAttack", false);
        }
        }
