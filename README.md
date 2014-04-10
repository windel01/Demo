<?php
//No direct access
defined('_JEXEC') or die("Access Deny");

$document = JFactory::getDocument();
$document->addScript(Juri::base().'components/com_lhcss/media/js/jquery.min.js');

?>



<table width="500" border="0">
	
	<form name = "courses_offered" id="courses_offered" method="POST">

		<!--Drop down list contain all the semesters-->
		<label for="semesters">Semesters</label>
		<select name = "semesters" id="semesters">
			<?php
			// Create object of the model and call function getSemester
		       $model = $this->getModel('retrievedata');
		       	$result=$model->getSemesters();
		       	// Loop semester to dropdown list
				foreach ($result as $key){
		    ?>
		    <option value="<?php echo $key->semester_id;?>"><?php echo $key->semester_id; ?></option>	    	 
		    <?php
			    }
		     ?>    
		</select>

		<!--Drop down list contain all the courses-->
		<label for="courses">Courses</label>
		<select name = "courses" id = "courses">				    
			<?php
			//Create object of the model and call function getCourses
				$model = $this->getModel('retrievedata');
				$result=$model->getCourses();
				// Loop semester to dropdown list
				foreach ($result as $key){
			?>
			<option value="<?php echo $key->course_name;?>"><?php echo $key->course_name; ?></option>
			<?php
				}
			?>
		</select>

		<!--Drop down list contain all the teachers-->
		<label for="teachers">Teachers</label>
		<select name= "teachers" id = "teachers">	
			<?php
			//Create object of the model and call function getCourses
				$model = $this->getModel('retrievedata');
				$result=$model->getTeachers();
				// Loop semester to dropdown list
				foreach ($result as $key){
			?>
			<option value="<?php echo $key->staff_id;?>"><?php echo $key->name; ?></option>
			<?php
				}
			?>
		</select>

		<button type = "button" name = "button" id="button">Submit</button>	
	</form>


<script type="text/javascript">
$(document).ready(function(){ 
   
   
    $("#button").on("click",function()  {
         var forminput = $("#courses_offered").serialize();
        //console.log(forminput);
        
            //var test = "This is a string wendel";  

           //console.log(semester);
        
    $.ajax({
    type: "post",
    url: "index.php?option=com_lhcss&task=coursesOffered",
    data:forminput,
    }).done(function(message){

        console.log(message);
    });
            
        
	});
   
   });

</script>
