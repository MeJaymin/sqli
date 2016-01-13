<?php
	
	if(!empty($_POST))
	{
		$msg="";
		
		
		
		
		if(empty($_POST['Name']))
		{
		echo "<script type='text/javascript'>alert('enter username')</script>";

		}
		
		if(empty($_POST['LastName'])){
				echo "<script type='text/javascript'>alert('enter last name!')</script>";
		}
		
		if($_POST['Email']!= $_POST['Cemail'])
		{
				$msg="enter same email";
					
		}
		if(empty($_POST['pass']))
		{
			echo "<script type='text/javascript'>alert('enter password')</script>";
		}
		
		if(strlen($_POST['pass'])>20)
		{
					echo "<script type='text/javascript'>alert('enter password under 20 characters')</script>";
		}
		
		if(is_numeric($_POST['Name']) || is_numeric($_POST['LastName']))
		{
					$msg="Enter name and last name in Characters";
		}
		
		
		if($msg!="")
		{
			header("location:register.php?error='er'".$msg);
		}
		else
		{
			$fnm=$_POST['Name'];
			$unm=$_POST['LastName'];
			$name = $fnm.' '.$unm;
			$pwd=$_POST['pass'];
			$email=$_POST['Email'];
			$ttype=$_POST['type'];
			
			
			
			
		
			$link=mysql_connect("localhost","root","")or die("Can't Connect...");
			
			mysql_select_db("wedding_planner",$link) or die("Can't Connect to Database...");
			
			$query="insert into user_regestration(fname,lname,password,email,type)
			values('$fnm','$unm','$pwd','$email','$ttype')";
			
			mysql_query($query,$link) or die("Can't Execute Query...".mysql_error());
			
			$q="select u_id from user_regestration where email='$email'";
			
			$res=mysql_query($q,$link) or die("wrong query");
			
			$row=mysql_fetch_assoc($res);

		
					
						header("location:log.php?reg=succ");
					
			
		}
			
	}
	else
	{
		header("location:index.php");
	}
?>
