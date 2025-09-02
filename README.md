# ballistics-solver
A C# script I made used for calculating the vector a projectile should be launched at to reach a certain position, even with varied height
<img width="512" height="379" alt="image" src="https://github.com/user-attachments/assets/24e7e97a-5411-47cf-a469-9a22594185b9" />
``` code
//C#
public static Vector2 ProjectileShootVector(this Vector2 startPos,Vector2 endPos,float velocity,float gravity,float maxQ = 1,float minQ = -Mathf.Infinity,bool best = true){
     float rx = endPos.x - startPos.x;
	 float x = Mathf.Abs(rx);
	 float h = -(endPos.y - startPos.y);
	 float phase = Mathf.Atan2(x,h) ;
	 float x_2 = Mathf.Pow(x,2);
	 float h_2 = Mathf.Pow(h,2);
	 float v_2 = Mathf.Pow(velocity,2);
	 gravity *= -Physics2D.gravity.y;

	 float X = ((gravity * x_2/v_2) - h) / Mathf.Sqrt(h_2 + x_2);
      if(X > 1 && !best){
		Debug.Log("No Trag : " + X);
		return Vector2.zero;
	  }
	 float angle = (Mathf.Acos(X > 1 ? x > h ? 1 : 0 : X) + phase)/2; 

	 return new Vector2(Mathf.Cos(angle) ,Mathf.Sin(angle)) * new Vector2(rx.Sign(),1);
	}
```
