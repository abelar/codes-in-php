prelim exam in webprog
============
//  form.php  //
<!doctype html>
<html>
	<head>
		<link rel="stylesheet" href="style.css" />
		<center>
			<img src = "logo.jpg " width = "150:" />
	
	<h1>K-12,TESDA AND CHED REGISTRATION FORM </h1>
		</center>
	</head>
        <body>
			<form  action = "submit.php" method="POST" >
				First Name: <input type="text" size="40" name="firstName" /><br>
				Last Name: <input type="text" size="40" name="lastName"/><br>
				Birthday:
					Month<select size = "1"name="month">
						<option	>choose</option>
							<?php for($i=12;$i>0;$i--):?>
								<option	value = "<?php echo $i; ?>"> <?php echo $i; ?> </option>
							<?php endfor; ?>
					</select>
					Day<select size = "1"name="day">
						<option	>choose</option>
							<?php for($i=31;$i>0;$i--):?>
								<option	value = "<?php echo $i; ?>"> <?php echo $i; ?> </option>
							<?php endfor; ?>
					</select> 
					Year<select size = "1"name="year">
						<option	>choose</option>
							<?php for($i=2014;$i>0;$i--):?>
								<option	value = "<?php echo $i; ?>"> <?php echo $i; ?> </option>
							<?php endfor; ?>
					</select> <br>		
				Address : <input type = "text" size = "40" name = "address"><br>	
				Contact Number: <input type = "text" size = "40" name = "contactNumber"/><br>	
				Father's Full Name :<input type = "text" size = "40" name = "fathers_full_name"/><br>	
				Father's Contact Number :<input type = "text" size = "40" name = "fathersContactnumber"/><br>	
				Mother's Full Name :<input type = "text" size = "40" name = "mothers_full_name"/><br>	
				Mother's Contact Number :<input type = "text" size = "40" name = "mothersContactnumber"/><br>	
				Student Type :
					<input type = "radio" size = "40" name = "studentType" value="K12" />K12
					<input type = "radio" size = "40" name = "studentType" value="TESDA" />TESDA
					<input type = "radio" size = "40" name = "studentType" value="CHED" />CHED<br>
			
				<input type = "submit" value = "SUBMIT" />
			</form>
		</body>
</html>

//  submit.php  //
<?php
	$fisrtName=(isset($_POST['firstName'])) ? $_POST['firstName'] : false;
	$lastName=$_POST['lastName'];
	$month =$_POST['month'];
	$day =$_POST['day'];
	$year=$_POST['year'];
	$birthday=$month."/".$day."/".$year;
	$address=$_POST['address'];
	$contactNumber=$_POST['contactNumber'];
	$fathers_full_name=$_POST['fathers_full_name'];
	$fathersContactnumber=$_POST['fathersContactnumber'];
	$mothers_full_name=$_POST['mothers_full_name'];
	$mothersContactNumber=$_POST['mothersContactnumber'];
	$studentType=$_POST['studentType'];

	if (isset($_POST) && !empty($studentType)) {
		switch ($studentType) {
			case 'K12':
				$filename = "K-12.csv";
				break;
			case 'TESDA':
				$filename = "TESDA.csv";
				break;
			case 'CHED':
				$filename = "CHED.csv";
				break;	
		}
		$data = array($fisrtName, $lastName, $birthday, $address, 
				$contactNumber, $fathers_full_name, $fathersContactnumber, $mothers_full_name,
				$mothersContactNumber, $studentType);
		$handler = fopen($filename, "a");
		fputcsv($handler, $data);
		fclose($handler);
	}
header ("Location:form.php");
?>

//  style.css //
body {
	font-family: Bookman Old Style, sans-serif;
	font-size: 12pt;
	color: #111111;
	background-color: lightgreen;
}
h1{
	color: brown;
	margin: .2em;
	line-height: 1em;
}

