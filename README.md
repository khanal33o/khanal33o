- 👋 Hi, I’m @khanal33o
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
khanal33o/khanal33o is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->index.php
<html>
<body>
<?php
include('header.php');
?>

<div class="content">
	<div class="wrap">
		<div class="content-top">
				<div class="listview_1_of_3 images_1_of_3">
					<h2 style="color:#555;">Upcoming Movies</h2>
					<?php 
					$qry3=mysqli_query($con,"SELECT * FROM tbl_news LIMIT 5");
					
					while($n=mysqli_fetch_array($qry3))
					{
					?>
				<div class="content-left">
					<div class="listimg listimg_1_of_2">
						 <img src="admin/<?php echo $n['attachment'];?>">
					</div>
					<div class="text list_1_of_2">
						  <div class="extra-wrap">
						  	<span style="text-color:#000" class="data"><strong><?php echo $n['name'];?></strong><br>
						  	<span style="text-color:#000" class="data"><strong>Cast :<?php echo $n['cast'];?></strong><br>
                                <div class="data">Release Date :<?php echo $n['news_date'];?></div>
                                
                                
                                
                                <span class="text-top"><?php echo $n['description'];?></span>
                          </div>
					</div>
					<div class="clear"></div>
				</div>
				<?php
				}
				?>
				
			
		</div>				
		<div class="listview_1_of_3 images_1_of_3">
					<h2 style="color:#555;">Movie Trailers</h2>
						<div class="middle-list">
					<?php 
					$qry4=mysqli_query($con,"SELECT * FROM tbl_movie ORDER BY rand() LIMIT 6");
				
					while($nm=mysqli_fetch_array($qry4))
					{
					?>
					
						<div class="listimg1">
							 <a target="_blank" href="<?php echo $nm['video_url'];?>"><img src="<?php echo $nm['image'];?>" alt=""/></a>
							 <a target="_blank" href="<?php echo $nm['video_url'];?>" class="link" style="text-decoration:none; font-size:14px;"><?php echo $nm['movie_name'];?></a>
						</div>
						<?php
					}
					?>
					</div>
					
					
		</div>			
		<?php include('movie_sidebar.php');?>
	</div>
</div>
<?php include('footer.php');?>
</div>
<?php include('searchbar.php');?>
about
<?php include('header.php');
	$qry2=mysqli_query($con,"select * from tbl_movie where movie_id='".$_GET['id']."'");
	$movie=mysqli_fetch_array($qry2);
	?>
<div class="content">
	<div class="wrap">
		<div class="content-top">
				<div class="section group">
					<div class="about span_1_of_2">	
						<h3 style="color:#444; font-size:23px;" class="text-center"><?php echo $movie['movie_name']; ?></h3>	
							<div class="about-top">	
								<div class="grid images_3_of_2">
									<img src="<?php echo $movie['image']; ?>" alt=""/>
								</div>
								<div class="desc span_3_of_2">
									<p class="p-link" style="font-size:15px"><b>Cast : </b><?php echo $movie['cast']; ?></p>
									<p class="p-link" style="font-size:15px"><b>Release Date : </b><?php echo date('d-M-Y',strtotime($movie['release_date'])); ?></p>
									<p style="font-size:15px"><?php echo $movie['desc']; ?></p>
									<a href="<?php echo $movie['video_url']; ?>" target="_blank" class="watch_but" style="text-decoration:none;">Watch Trailer</a>
								</div>
								<div class="clear"></div>
							</div>
							<?php $s=mysqli_query($con,"select DISTINCT theatre_id from tbl_shows where movie_id='".$movie['movie_id']."'");
							if(mysqli_num_rows($s))
							{?>
							<table class="table table-hover table-bordered text-center">
								<h3 style="color:#444;" class="text-center">Available Shows</h3>

								<thead>
										<tr>
											<th class="text-center" style="font-size:16px;"><b>Theatre</b></th>
											<th class="text-center" style="font-size:16px;"><b>Show Timings</b></th>
										</tr>
									</thead>
							<?php

							
								
								while($shw=mysqli_fetch_array($s))
								{
									
									$t=mysqli_query($con,"select * from tbl_theatre where id='".$shw['theatre_id']."'");
									$theatre=mysqli_fetch_array($t);
									?>
									

									<tbody>
									<tr>
										<td >
											<?php echo $theatre['name'].", ".$theatre['place'];?>
										</td>
										<td>
											<?php $tr=mysqli_query($con,"select * from tbl_shows where movie_id='".$movie['movie_id']."' and theatre_id='".$shw['theatre_id']."'");
											while($shh=mysqli_fetch_array($tr))
											{
												$ttm=mysqli_query($con,"select  * from tbl_show_time where st_id='".$shh['st_id']."'");
												$ttme=mysqli_fetch_array($ttm);
												
												?>
												
												<a href="check_login.php?show=<?php echo $shh['s_id'];?>&movie=<?php echo $shh['movie_id'];?>&theatre=<?php echo $shw['theatre_id'];?>"><button class="btn btn-default"><?php echo date('h:i A',strtotime($ttme['start_time']));?></button></a>
												<?php
											}
											?>
										</td>
									</tr>
									</tbody>
									<?php
								}
							?>
						</table>
							<?php
							}
						
							else
							{
								?>
								<h3 style="color:#444; font-size:23px;" class="text-center">Currently there are no any shows available!</h3>
								<p class="text-center">Please check back later!</p>
								<?php
							}
							?>
						
					</div>			
				<?php include('movie_sidebar.php');?>
			</div>
				<div class="clear"></div>		
			</div>
	</div>
</div>
<?php include('footer.php');?>
login
<?php
session-start();
include-once("../include/db_connect.php");
if ($_REQUEST[act]=="check_admin")
{
check_admin();
}
if($_REQUEST[act]=="logout")
{
logout();
}
bank
<?php include('header.php');?>
</div>
<div class="content">
	<div class="wrap">
		<div class="content-top">
			<h3>Movies</h3>
                        <h4>adminJanak</h4>
			xvc
			</div>
			
		<div class="clear"></div>	
		
	</div>
<?php include('footer.php');?>
</div>
booking
<?php include('header.php');
if(!isset($_SESSION['user']))
{
	header('location:login.php');
}
	$qry2=mysqli_query($con,"select * from tbl_movie where movie_id='".$_SESSION['movie']."'");
	$movie=mysqli_fetch_array($qry2);
	?>
<div class="content">
	<div class="wrap">
		<div class="content-top">
				<div class="section group">
					<div class="about span_1_of_2">	
						<h3><?php echo $movie['movie_name']; ?></h3>	
							<div class="about-top">	
								<div class="grid images_3_of_2">
									<img src="<?php echo $movie['image']; ?>" alt=""/>
								</div>
								<div class="desc span_3_of_2">
									<p class="p-link" style="font-size:15px"><b>Cast : </b><?php echo $movie['cast']; ?></p>
									<p class="p-link" style="font-size:15px"><b>Release Date : </b><?php echo date('d-M-Y',strtotime($movie['release_date'])); ?></p>
									<p style="font-size:15px"><?php echo $movie['desc']; ?></p>
									<a href="<?php echo $movie['video_url']; ?>" target="_blank" class="watch_but">Watch Trailer</a>
								</div>
								<div class="clear"></div>
							</div>
							<table class="table table-hover table-bordered text-center">
							<?php
								$s=mysqli_query($con,"select * from tbl_shows where s_id='".$_SESSION['show']."'");
								$shw=mysqli_fetch_array($s);
								
									$t=mysqli_query($con,"select * from tbl_theatre where id='".$shw['theatre_id']."'");
									$theatre=mysqli_fetch_array($t);
									?>
									<tr>
										<td class="col-md-6">
											Theatre
										</td>
										<td>
											<?php echo $theatre['name'].", ".$theatre['place'];?>
										</td>
										</tr>
										<tr>
											<td>
												Screen
											</td>
										<td>
											<?php 
												$ttm=mysqli_query($con,"select  * from tbl_show_time where st_id='".$shw['st_id']."'");
												
												$ttme=mysqli_fetch_array($ttm);
												
												$sn=mysqli_query($con,"select  * from tbl_screens where screen_id='".$ttme['screen_id']."'");
												
												$screen=mysqli_fetch_array($sn);
												echo $screen['screen_name'];
							
												?>
										</td>
									</tr>
									<tr>
										<td>
											Date
										</td>
										<td>
											<?php 
											if(isset($_GET['date']))
							{
								$date=$_GET['date'];
							}
							else
							{
								if($shw['start_date']>date('Y-m-d'))
								{
									$date=date('Y-m-d',strtotime($shw['start_date'] . "-1 days"));
								}
								else
								{
									$date=date('Y-m-d');
								}
								$_SESSION['dd']=$date;
							}
							?>
							<div class="col-md-12 text-center" style="padding-bottom:20px">
								<?php if($date>$_SESSION['dd']){?><a href="booking.php?date=<?php echo date('Y-m-d',strtotime($date . "-1 days"));?>"><button class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i></button></a> <?php } ?><span style="cursor:default" class="btn btn-default"><?php echo date('d-M-Y',strtotime($date));?></span>
								<?php if($date!=date('Y-m-d',strtotime($_SESSION['dd'] . "+4 days"))){?>
								<a href="booking.php?date=<?php echo date('Y-m-d',strtotime($date . "+1 days"));?>"><button class="btn btn-default"><i class="glyphicon glyphicon-chevron-right"></i></button></a>
								<?php }
								$av=mysqli_query($con,"select sum(no_seats) from tbl_bookings where show_id='".$_SESSION['show']."' and ticket_date='$date'");
								$avl=mysqli_fetch_array($av);
								?>
							</div>
										</td>
									</tr>
									<tr>
										<td>
											Show Time
										</td>
										<td>
											<?php echo date('h:i A',strtotime($ttme['start_time']))." ".$ttme['name'];?> Show
										</td>
									</tr>
									<tr>
										<td>
											Number of Seats
										</td>
										<td>
											<form  action="process_booking.php" method="post">
												<input type="hidden" name="screen" value="<?php echo $screen['screen_id'];?>"/>
											<input type="number" required tile="Number of Seats" max="<?php echo $screen['seats']-$avl[0];?>" min="0" name="seats" class="form-control" value="1" style="text-align:center" id="seats"/>
											<input type="hidden" name="amount" id="hm" value="<?php echo $screen['charge'];?>"/>
											<input type="hidden" name="date" value="<?php echo $date;?>"/>
										</td>
									</tr>
									<tr>
										<td>
											Amount
										</td>
										<td id="amount" style="font-weight:bold;font-size:18px">
											Rs <?php echo $screen['charge'];?>
										</td>
									</tr>
									<tr>
										<td colspan="2"><?php if($avl[0]==$screen['seats']){?><button type="button" class="btn btn-danger" style="width:100%">House Full</button><?php } else { ?>
										<button class="btn btn-info" style="width:100%">Book Now</button>
										<?php } ?>
										</form></td>
									</tr>
						<table>
							<tr>
								<td></td>
							</tr>
						</table>
					</div>			
				<?php include('movie_sidebar.php');?>
			</div>
				<div class="clear"></div>		
			</div>
	</div>
</div>
<?php include('footer.php');?>
<script type="text/javascript">
	$('#seats').change(function(){
		var charge=<?php echo $screen['charge'];?>;
		amount=charge*$(this).val();
		$('#amount').html("Rs "+amount);
		$('#hm').val(amount);
                $('admin') management(Janak);
	});
</script>
cancle
<?php
session_start();
include('config.php');
mysqli_query($con,"delete from tbl_bookings where book_id='".$_GET['id']."'");
$_SESSION['success']="Booking Cancelled Successfully";
header('location:profile.php');
?>
check login
<?php
session_start();
$-SESSION['admin']=$_GET['admin'];
$_SESSION['show']=$_GET['show'];
$_SESSION['movie']=$_GET['movie'];
$_SESSION['theatre']=$_GET['theatre'];
if(isset($_SESSION['user']))
{
    header('location:booking.php');
}
else
{
    header('location:login.php');
}
?>
compayment
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
<?php
session_start();
if(!isset($_SESSION['user']))
{
	header('location:login.php');
}
include('config.php');
extract($_POST);

//OTP Code
if($otp=="123456")
{
    $bookid="BKID".rand(012,0508,0535960);
    mysqli_query($con,"INSERT into tbl_bookings values(NULL,'$bookid','".$_SESSION['theatre']."','".$_SESSION['user']."','".$_SESSION['show']."','".$_SESSION['screen']."','".$_SESSION['seats']."','".$_SESSION['amount']."','".$_SESSION['date']."',CURDATE(),'1')");
    $_SESSION['success']="Bookings Done";
}
else
{
    $_SESSION['error']="Payment Failed";
}
?>
<body><table align='center'><tr><td><STRONG>Transaction is being processed,</STRONG></td></tr><tr><td><font color='blue'>Please Wait <i class="fa fa-spinner fa-pulse fa-fw"></i>
<span class="sr-only"></font></td></tr><tr><td>(Do not 'RELOAD' this page or 'CLOSE' this page)</td></tr></table><h2>
<script>
    setTimeout(function(){ window.location="profile.php"; }, 3000);
</script>
cong
<?php
    $host = "localhost";
    $user = "root";                     
    $pass = "";                                  
    $db = "movietheatredb";
    $port = 3306;
     $con = mysqli_connect($host, $user, $pass, $db, $port)or die(mysql_error());
?>
contac
<!--
Author: W3layouts
Author URL: http://w3layouts.com
License: Creative Commons Attribution 3.0 Unported
License URL: http://creativecommons.org/licenses/by/3.0/
-->
<!DOCTYPE HTML>
<html>
<head>
<title>Free Theater Website Template | Contact :: w3layouts</title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<link rel="stylesheet" href="css/style.css" type="text/css" media="all" />
<script src='http://ajax.googleapis.com/ajax/libs/jquery/1.5.2/jquery.min.js'></script>
<script src='js/jquery.color-RGBa-patch.js'></script>
<script src='js/example.js'></script>
</head>
<body>
<div class="header">
	<div class="header-top">
		<div class="wrap">
			<div class="h-logo">
			<a href="index.php"><img src="images/logo.png" alt=""/></a>
		</div>
			  <div class="nav-wrap">
					<ul class="group" id="example-one">
			           <li><a href="index.php">Home</a></li>
			           <li><a href="about.php">About</a></li>
			  		   <li><a href="movies_events.php">Movies & Events</a></li>
			  		   <li class="current_page_item"><a href="contact.php">Contact</a></li>
			        </ul>
			  </div>
 			<div class="clear"></div>
   		</div>
    </div>
<div class="block">
	<div class="wrap">
		
        <form action="#" id="reservation-form" method="post">
		       <fieldset>
		                <div class="field">
			                 <label>Find a Movie:</label>
			                  <select class="select2">
			                    <option>Movie list</option>
			                  </select>
			            </div>
		                <div class="field1">
			                   <label>Search</label>
			                  <select class="select1">
			                    <option>Movies or Actors</option>
			                  </select>
		                </div>
		       </fieldset>
            </form>
            <div class="clear"></div>
   </div>
</div>
</div>
<div class="content">
	<div class="wrap">
		<div class="content-top">
				<div class="section group">
				<div class="col span_2_of_3">
				  <div class="contact-form">
				  	<h3>Contact Us</h3>
					    <form action="process_contact.php" method="post" name="form11">
					    	<div>
						    	<span><label>NAME</label></span>
						    	<span><input type="text" value="" required name="name"></span>
						    </div>
						    <div>
						    	<span><label>E-MAIL</label></span>
						    	<span><input type="text" value="" required name="email"></span>
						    </div>
						    <div>
						     	<span><label>MOBILE.NO</label></span>
						    	<span><input type="number" value="" required name="mobile"></span>
						    </div>
						    <div>
						    	<span><label>SUBJECT</label></span>
						    	<span><textarea required name="subect"> </textarea></span>
						    </div>
						   <div>
						   		<span><input type="submit">Submit</span>
						  </div>
					    </form>
				  </div>
  				</div>
				<div class="col span_1_of_3">
					<div class="contact_info">
    	 				<h3>Find Us Here</h3>
					    	  <div class="map">
							   	    <iframe width="100%" height="175" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" src="https://maps.google.co.in/maps?f=q&amp;source=s_q&amp;hl=en&amp;geocode=&amp;q=Lighthouse+Point,+FL,+United+States&amp;aq=4&amp;oq=light&amp;sll=26.275636,-80.087265&amp;sspn=0.04941,0.104628&amp;ie=UTF8&amp;hq=&amp;hnear=Lighthouse+Point,+Broward,+Florida,+United+States&amp;t=m&amp;z=14&amp;ll=26.275636,-80.087265&amp;output=embed"></iframe><br><small><a href="https://maps.google.co.in/maps?f=q&amp;source=embed&amp;hl=en&amp;geocode=&amp;q=Lighthouse+Point,+FL,+United+States&amp;aq=4&amp;oq=light&amp;sll=26.275636,-80.087265&amp;sspn=0.04941,0.104628&amp;ie=UTF8&amp;hq=&amp;hnear=Lighthouse+Point,+Broward,+Florida,+United+States&amp;t=m&amp;z=14&amp;ll=26.275636,-80.087265" style="color:#666;text-align:left;font-size:12px">View Larger Map</a></small>
							  </div>
      				</div>
      			<div class="company_address">
				     	<h3>Company Information :</h3>
						    	<p>500 Lorem Ipsum Dolor Sit,</p>
						   		<p>22-56-2-9 Sit Amet, Lorem,</p>
						<p>Phone:(00) 9823477036</p>
				   		<p>Fax: (000) 000 00 00 0</p>
				 	 	<p>Email: <span>info@mycompany.com</span></p>
				   		<p>Follow on: <span>Facebook</span>, <span>Twitter</span></p>
				   </div>
				 </div>
			  </div>
				<div class="clear"></div>		
			</div>
	</div>
</div>
<div class="footer">
	<div class="wrap">
			<div class="footer-top">
				<div class="col_1_of_4 span_1_of_4">
					<div class="footer-nav">
		                <ul>
		                   <li><a href="">Our Tips of gallery Template diam</a></li>
		                    <li><a href="">Our Tips of gallery Template diam</a></li>
		                     <li><a href="">Our Tips of gallery Template diam</a></li>
		                       <li><a href="">Our Tips of gallery Template diam</a></li>
		                   </ul>
		              </div>
				</div>
				<div class="col_1_of_4 span_1_of_4">
					<div class="textcontact">
						<p>consectetuer adipiscing elit,<br>
						consectetuer<br>
						Ph: 9823477036.<br>
						Email:Support(at)Fotoria-scope.com<br>
						</p>
					</div>
				</div>
				<div class="col_1_of_4 span_1_of_4">
					<div class="call_info">
						<p class="txt_3">Call us toll free:</p>
						<p class="txt_4">98634336</p>
					</div>
				</div>
				<div class="col_1_of_4 span_1_of_4">
					<div class=social>
						<a href="#"><img src="images/fb.png" alt=""/></a>
						<a href="#"><img src="images/tw.png" alt=""/></a>
						<a href="#"><img src="images/dribble.png" alt=""/></a>
						<a href="#"><img src="images/pinterest.png" alt=""/></a>
					</div>
				</div>
				<div class="clear"></div>
			</div>
		</div>
	</div>
	<div class="footer-bottom">
	<div class="wrap">
	<div class="copy">
		<p>All rights Reserved | Design by <a href="http://w3layouts.com">W3Layouts</a></p>
	</div>
 	</div>
</div>
</body>
</html>
foot
<div class="footer">
	<div class="wrap">
			<div class="footer-top">
				<div class="col_1_of_4 span_1_of_4">
					<div class="footer-nav">
		                <ul>
		                   <li><a href="index.php" style="text-decoration:none;">Home</a></li>
			  		   <li><a href="movies_events.php" style="text-decoration:none;">Movies</a></li>
			  		   <li><a href="login.php" style="text-decoration:none;">Login</a></li>
		                   </ul>
		              </div>
				</div>
				<div class="col_1_of_4 span_1_of_4">
					<div class="textcontact">
						<p>Theatre Assistance<br>
						Online Movie Theatre Booking System<br>
						Ph: 9863464336<br>
						</p>
					</div>
				</div>
				<div class="col_1_of_4 span_1_of_4">
					<div class="call_info">
						<p class="txt_3">Call us toll free:</p>
						<p class="txt_4">9823477036</p>
					</div>
				</div>
				<div class="col_1_of_4 span_1_of_4">
					<div class=social>
						<a href="#"><img src="images/fb.png" alt=""/></a>
						<a href="#"><img src="images/tw.png" alt=""/></a>
						<a href="#"><img src="images/dribble.png" alt=""/></a>
						<a href="#"><img src="images/pinterest.png" alt=""/></a>
                                                 <a href="#"><img src="image/dmin/dribble.png" alt=""/></a>
					</div>
				</div>
				<div class="clear"></div>
			</div>
		</div>
	</div>
</body>
</html>

<style>
.content {
	padding-bottom:0px !important;

}
#form111 {
                width:500px;
                margin:50px auto;
}
#search111{
                padding:8px 15px;
                background-color:#fff;
                border:0px solid #dbdbdb;
}
#button111 {
                position:relative;
                padding:6px 15px;
                left:-8px;
                border:2px solid #ca072b;
                background-color:#ca072b;
                color:#fafafa;
}
#button111:hover  {
                background-color:#b70929;
                color:white;
}

</style>

<script src="js/auto-complete.js"></script>
 <link rel="stylesheet" href="css/auto-complete.css">
    <script>
        var demo1 = new autoComplete({
            selector: '#search111',
            minChars: 1,
            source: function(term, suggest){
                term = term.toLowerCase();
                <?php
						$qry2=mysqli_query($con,"select * from tbl_movie");
						?>
               var string="";
                <?php $string="";
                while($ss=mysqli_fetch_array($qry2))
                {
                
                $string .="'".strtoupper($ss['movie_name'])."'".",";
                //$string=implode(',',$string);
                
              
                }
                ?>
                //alert("<?php echo $string;?>");
              var choices=[<?php echo $string;?>];
                var suggestions = [];
                for (i=0;i<choices.length;i++)
                    if (~choices[i].toLowerCase().indexOf(term)) suggestions.push(choices[i]);
                suggest(suggestions);
            }
        });
    </script>
    form
    <?php
/**
* class for build form
*/ 
class formBuilder
{
    var $form_id; // form id
    var $validators=" ";
	function build($type,$name,$id,$class,$placeholder,$opt)//for create input types with given atributes
	{
		if ($type=="text") // if text box
		{
			$input="<input type='text' name='$name' id='$id' class='$class' placeholder='$placeholder' $opt>";
            echo $input;
		}
        if ($type=="date") // if text box
		{
			$input="<input type='date' name='$name' id='$id' class='$class' placeholder='$placeholder' $opt>";
            echo $input;
		}
        if ($type=="number") // if number box
		{
			$input="<input type='number' name='$name' id='$id' class='$class' $opt>";
            echo $input;
		}
        if ($type=="email") // if email
		{
			$input="<input type='email' name='$name' id='$id' class='$class' $opt>";
            echo $input;
		}
        if ($type=="password") // if password
		{
			$input="<input type='password' name='$name' id='$id' class='$class' placeholder='$placeholder' $opt>";
            echo $input;
		}
        if ($type=="radio") // if radio button
		{
			$input="<input type='radio' name='$name' id='$id' class='$class' $opt>";
            echo $input;
		}
        if ($type=="checkbox") // if checkbox
		{
			$input="<input type='checkbox' name='$name' id='$id' class='$class' $opt>";
            echo $input;
		}
        if ($type=="textarea") //if textarea
		{
			$input="<textarea name='$name' id='$id' class='$class' placeholder='$placeholder' $opt></textarea>";
            echo $input;
		}
        if ($type=="submit") // if submit
		{
			$input="<button type='submit' class='$class'>$opt</button>";
            echo $input;
		}
        if ($type=="file") // if text box
		{
			$input="<input type='file' name='$name' id='$id' class='$class' placeholder='$placeholder' $opt>";
            echo $input;
		}
    }
    function validate($name,$rules) // function for validation name: name of the field, rules: validation rules
    {
       
        $this->validators=$this->validators."
            $name: {
            verbose: false,
                validators: {";
        if (in_array("required",$rules)) // if rules array have value required
        {
            $label=$rules["label"];
           $this->validators=$this->validators."notEmpty: {
                        message: 'The $label is required and can\'t be empty'
                    }," ;
        }
        if (array_key_exists("min",$rules) && array_key_exists("max",$rules)) // if rules array have value min and max
        {
            $label=$rules["label"];
            $min=$rules["min"];
            $max=$rules["max"];
            $this->validators=$this->validators."stringLength: {
                    min: $min,
                    max: $max,
                    message: 'The $label must be more than $min and less than $max characters long'
                }," ;
           
        }
        else if(array_key_exists("max",$rules)) // if rules array have value max
        {
            $label=$rules["label"];
            $max=$rules["max"];
            $this->validators=$this->validators."stringLength: {
                    max: $max,
                    message: 'The $label must be less than $max characters long'
                }," ;
        }
        else if(array_key_exists("min",$rules)) // if rules array have value min
        {
            $label=$rules["label"];
            $min=$rules["min"];
            $this->validators=$this->validators."stringLength: {
                    min: $min,
                    message: 'The $label must be more than $min characters long'
                }," ;
        }
        if (array_key_exists("regexp",$rules)) // if rules array have value regular expression validation
        {
            $label=$rules["label"];
            $exp=$rules["regexp"];
            switch($exp) // selecting regular expression types
            {
                case "name": // if validation for name
                    $expression='/^[a-zA-Z ]+$/';
                    $err_msg="The $label can only consist of alphabets";
                    break;
                case "age":
                    $expression='/^(0?[0-9]?[0-9]|1[01][0-1]|11[0-1])$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "address":
                    $expression='/^[a-zA-Z0-9,\n ]+$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "place":
                    $expression='/^[a-zA-Z ,]+$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "pin":
                    $expression='/^[1-9][0-9]{5}$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "mobile":
                    $expression='/^([0|\+[9][1]{1,5})?([7-9][0-9]{9})$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "phone":
                    $expression='/^[0-9]\d{2,4}-\d{6,8}$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "number":
                    $expression='/^[0-9 ]+$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "text":
                    $expression='/^[a-zA-Z,. ]+$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "year":
                    $expression='/^[1-2]{1}[0-9]{3}$/';
                    $err_msg="Enter a valid $label";
                    break;
                case "url":
                    $expression='/@^(http\:\/\/|https\:\/\/)?([a-z0-9][a-z0-9\-]*\.)+[a-z0-9][a-z0-9\-]*$@i/';
                    $err_msg="Enter a valid $label";
                    break;
            }
            $this->validators=$this->validators."regexp: {
                        regexp: $expression,
                        message: '$err_msg'
                    },";
        }
        if (in_array("email",$rules)) // if rules array have value required
        {
            $this->validators=$this->validators."emailAddress: {
                        message: 'The input is not a valid email address'
                    },";
            
        }
        if (array_key_exists("identical",$rules)) // if the field identical to another
        { 
            $identical=$rules["identical"];
            $identical_field= explode(" ",$identical);// first array value is the field which identical,second is the label of thal field
            $idl=$identical_field[0];
            $label=$rules["label"];
            $msg="";
            for($i=1;$i<sizeof($identical_field);$i++) //for extracting message
            {
                $msg=$msg.' '.$identical_field[$i];
            }
            $this->validators=$this->validators."identical: {
                        field: '$idl',
                        message: 'The $msg and $label are not the same'
                    },";
        }
        if (array_key_exists("different",$rules)) // if the field must different to another
        { 
            $different=$rules["different"];
            $label=$rules["label"];
            $different_field= explode(" ",$different); //first array value is the field which different,second is the label of thal field
            $msg="";
            $dff=$different_field[0];
            for($i=1;$i<sizeof($different_field);$i++)// for extracting message
            { 
                $msg=$msg.' '.$different_field[$i];
            }
            $this->validators=$this->validators."different: {
                        field: '$dff',
                        message: 'The $label and $msg must be different'
                    },";
        }
        if (array_key_exists("remote",$rules)) // if the field has remote validation
        {
            $remote=$rules["remote"];
            $label=$rules["label"];
            $this->validators=$this->validators."remote: {
                        message: 'Enter the $label',
                        url: '$remote',
                        type: 'POST',
                        delay: 2000
                    },";
        }
        $this->validators=rtrim($this->validators,",");
        $this->validators=$this->validators." } },";
        //echo $this->validators;
    }
    function applyvalidations($form_id)
    { 
        $header="
            $(document).ready(function() {
            $('#$form_id').bootstrapValidator({
            fields: {";
        $footer="}
            });
            });
            ";
        $this->validators=rtrim($this->validators,",");
        echo $header;
        echo $this->validators;
        echo $footer;
        $this->validators="";//clearing for nexe form in same page
    }
    
}
?>
head
<?php
include('config.php');
session_start();
date_default_timezone_set('Asia/Kathmandu');
?>

<!DOCTYPE HTML>
<html>
<head>
<title>omg</title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<link rel="stylesheet" href="css/style.css" type="text/css" media="all" />
<link rel="stylesheet" href="css/flexslider.css" type="text/css" media="all" />
<link type="text/css" rel="stylesheet" href="http://www.dreamtemplate.com/dreamcodes/tabs/css/tsc_tabs.css" />
<link rel="stylesheet" href="css/tsc_tabs.css" type="text/css" media="all" />
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script src='js/jquery.color-RGBa-patch.js'></script>
<script src='js/example.js'></script>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>
<body>
<div class="header">
	<div class="header-top">
		<div class="wrap">
			<div class="h-logo">
			<a href="index.php"><img src="images/t-logo.png" alt="Logo Image Here"/></a>
		</div>
			  <div class="nav-wrap">
					<ul class="group" id="example-one" ></ul> 
                                        <li><a href="index.php" >admin</a></li>
                                        <li><a href="admin_event.php">admin</a></li>
                                        <li><?php if(isset($_SESSION['admin'])){
                                         $us=mysqli_query($con,"select* form admin tbl_registration where admin_id='".$_SESSION['admin']."'");$user=mysqli_fetch_array($us);?><a href="profile.php"><?php echo $user['name'];?></a><a href="logout.php">Logout</a><?php }
			          else{?><a href="login.php">Login</a> <a href="registration.php">Register</a><?php }?></li>
			        </ul> <li><a href="index.php" >Home</a></li>
			  		   <li><a href="movies_events.php">Movies</a></li>
			  		   <li><?php if(isset($_SESSION['user'])){
			  		   $us=mysqli_query($con,"select * from tbl_registration where user_id='".$_SESSION['user']."'");
        $user=mysqli_fetch_array($us);?><a href="profile.php"><?php echo $user['name'];?></a><a href="logout.php">Logout</a><?php }else{?><a href="login.php">Login</a> <a href="registration.php">Register</a><?php }?></li>
			        </ul>
			  </div>
 			<div class="clear"></div>
			
   		</div>
		
    </div>
     			<div class="clear"></div>
   	
<div class="block">
	<div class="wrap">
		
        <form action="process_search.php" id="reservation-form" method="post" onsubmit="myFunction()">
		       <fieldset>
		       	<div class="field" >
		       	
		       		     
                                <input type="text" placeholder="Enter A Movie Name" style="height:30px;width:300px"  required id="search111" name="search">
                                
                                <input type="submit" value="Search" style="height:34px;padding-top:3px" id="button111">
    </div>       	
    movie side
    
 			<div class="listview_1_of_3 images_1_of_3">
					<h2 style="color:#555;">Films in Theaters</h2>
					
					<?php
          	 $today=date("Y-m-d");
          	$qry2=mysqli_query($con,"select * from  tbl_movie where status='0' order by rand() limit 5");
						
          	  while($m=mysqli_fetch_array($qry2))
                   {
                    ?>
            <div class="content-left">
					<div class="listimg listimg_1_of_2">
					<?php
						
						?>
						 <a href="about.php?id=<?php echo $m['movie_id'];?>"><img src="<?php echo $m['image'];?>"></a>
					</div>
					<div class="text list_1_of_2">
						  <div class="extra-wrap1">
                                         <a href="about.php?id=<?php echo $m['movie_id'];?>" class="link4" style="text-decoration:none; font-size:18px;"><?php echo $m['movie_name'];?></a><br>
                                        <span class="data">Release Date: <?php echo $m['release_date'];?></span><br>
                                        Cast: <Span class="data"><?php echo $m['cast'];?></span><br>
                                        Description: <span" class="color2" style="text-decoration:none;"><?php echo $m['desc'];?></span><br>
                                    </div>
					</div>
					
					<div class="clear"></div>
				</div>
  	    <?php
  	    	}
  	    	?>
					
					
				
				
					
					
				
				
				
				
				</div>		
				<div class="clear"></div>		
			movie event
      <?php include('header.php');?>
</div>
<div class="content">
	<div class="wrap">
		<div class="content-top">
			<center><h1 style="color:#555;">(NOW SHOWING)</h1></center>
			
			<?php
          	 $today=date("Y-m-d");
          	 $qry2=mysqli_query($con,"select * from  tbl_movie ");
		
          	  while($m=mysqli_fetch_array($qry2))
                   {
                    ?>
                    
                    <div class="col_1_of_4 span_1_of_4">
					<div class="imageRow">
						  	<div class="single">
						  		<?php
						
						?>
						  		<a href="about.php?id=<?php echo $m['movie_id'];?>"><img src="<?php echo $m['image'];?>" alt="" /></a>
						  	</div>
						  	<div class="movie-text">
						  		<h4 class="h-text"><a href="about.php?id=<?php echo $m['movie_id'];?>" style="text-decoration:none;"><?php echo $m['movie_name'];?></a></h4>
						  		Cast: <Span class="color2" style="text-decoration:none;"><?php echo $m['cast'];?></span><br>
						  		
						  	</div>
		  				</div>
		  		</div>
		  		
  	    <?php
  	    	}
  	    	?>
			
			</div>
				<div class="clear"></div>		
			</div>
			<?php include('footer.php');?>
      msgbox
      <?php

if(isset($_SESSION['success']))
{?>
    <div class="alert alert-success alert-dismissible" id='hideMe'>
        <button type="button" class="close" data-dismiss="alert" aria-hidden="true">&times;</button>
        <h4><i class="icon fa fa-check"></i> Success!</h4>
        <?php echo $_SESSION['success'];?>
    </div>
<?php 

    unset($_SESSION['success']);
}
if(isset($_SESSION['error']))
{?>
    <div class="alert alert-danger alert-dismissible">
        <button type="button" class="close" data-dismiss="alert" aria-hidden="true">&times;</button>
        <h4><i class="icon fa fa-ban"></i> Alert!</h4>
        <?php echo $_SESSION['error'];?>
    </div>
<?php
unset($_SESSION['error']);
}
?>
booking process
<?php include('header.php');
if(!isset($_SESSION['user']))
{
	header('location:login.php');
}?>
<link rel="stylesheet" href="validation/dist/css/bootstrapValidator.css"/>
    
<script type="text/javascript" src="validation/dist/js/bootstrapValidator.js"></script>
  <!-- =============================================== -->
  <?php
    include('form.php');
    $frm=new formBuilder;      
  ?> 
</div>
<div class="content">
	<div class="wrap">
		<div class="content-top">
			<h3>Payment/Booking</h3>
			<form action="bank.php" method="post" id="form1">
			<div class="col-md-4 col-md-offset-4" style="margin-bottom:50px">
			<div class="form-group">
   <label class="control-label">Name on Card</label>
    <input type="text" class="form-control" name="name">
</div>
<div class="form-group">
   <label class="control-label">Card Number</label>
    <input type="text" class="form-control" name="number" required title="Enter 16 digit card number">
  
</div>      
<div class="form-group">
   <label class="control-label">Expiration date</label>
    <input type="date" class="form-control" name="date">
</div>
<div class="form-group">
   <label class="control-label">CVV</label>
    <input type="text" class="form-control" name="cvv">
</div>
<div class="form-group">
    <button class="btn btn-success">Make Payment</button>
    </form>
</div>
</div>
			</div>
			
		<div class="clear"></div>	
		
	</div>
<?php include('footer.php');?>
</div>
<?php
    session_start();
    extract($_POST);
    include('config.php');
    $_SESSION['screen']=$screen;
    $_SESSION['seats']=$seats;
    $_SESSION['amount']=$amount;
    $_SESSION['date']=$date;
    header('location:bank.php');
?>
<script>
        $(document).ready(function() {
            $('#form1').bootstrapValidator({
            fields: { 
            name: {
            verbose: false,
                validators: {notEmpty: {
                        message: 'The Name is required and can\'t be empty'
                    },regexp: {
                        regexp: /^[a-zA-Z ]+$/,
                        message: 'The Name can only consist of alphabets'
                    } } },
            number: {
            verbose: false,
                validators: {notEmpty: {
                        message: 'The Card Number is required and can\'t be empty'
                    },stringLength: {
                    min: 16,
                    max: 16,
                    message: 'The Card Number must 16 characters long'
                },regexp: {
                        regexp: /^[0-9 ]+$/,
                        message: 'Enter a valid Card Number'
                    } } },
            date: {
            verbose: false,
                validators: {notEmpty: {
                        message: 'The Expire Date is required and can\'t be empty'
                    } } },
            cvv: {
            verbose: false,
                validators: {notEmpty: {
                        message: 'The cvv is required and can\'t be empty'
                    },stringLength: {
                    min: 3,
                    max: 3,
                    message: 'The cvv must 3 characters long'
                },regexp: {
                        regexp: /^[0-9 ]+$/,
                        message: 'Enter a valid cvv'
                    } } }}
            });
            });

</script>
process cont
<?php
    include('config.php');
    extract($_POST);
   $qry=mysqli_query($con,"insert into tbl_contact values(NULL,'$name','$email',$mobile','$subject')");
    //echo $qry;
    //header('location:contact.php');
?>
login process
<?php
include('config.php');
session_start();
$email = $_POST["Email"];
$pass = $_POST["Password"];
$qry=mysqli_query($con,"select * from tbl_login where username='$email' and password='$pass'");
if(mysqli_num_rows($qry))
{
	$usr=mysqli_fetch_array($qry);
	if($usr['user_type']==2)
	{
		$_SESSION['user']=$usr['user_id'];
		if(isset($_SESSION['show']))
		{
			header('location:booking.php');
		}
		else
		{
			header('location:index.php');
		}
	}
	else
	{
		$_SESSION['error']="Login Failed!";
		header("location:login.php");
	}
	
}
else
{
	$_SESSION['error']="Login Failed!";
	header("location:login.php");
}
?>


pocee register
    session_start();
    include('config.php');
    extract($_POST);
    mysqli_query($con,"insert into  tbl_registration values(NULL,'$name','$email','$phone','$age','gender')");
    $id=mysqli_insert_id($con);
    mysqli_query($con,"insert into  tbl_login values(NULL,'$id','$email','$password','2')");
    $_SESSION['user']=$id;
    $-SESSION['admin'="janak khanal rr colage 9823477036";
    header('location:index.php');

searching
<?php include('header.php');
extract($_POST);
?>
</div>
<div class="content">
	<?php 
	// print_r($rs);
	?>
	<div class="wrap">
		<div class="content-top">
			<h3>Movies</h3>
			
			<?php
          	 $today=date("Y-m-d");
          	$qry2=mysqli_query($con,"select DISTINCT movie_name,movie_id,image,cast from tbl_movie where movie_name='".$search."'");
						
          	  while($m=mysqli_fetch_array($qry2))
                   {
                    ?>
                    
                    <div class="col_1_of_4 span_1_of_4">
					<div class="imageRow">
						  	<div class="single">
						  	
						  		<a href="about.php?id=<?php echo $m['movie_id'];?>" rel="lightbox"><img src="<?php echo $m['image'];?>" alt="" /></a>
						  	</div>
						  	<div class="movie-text">
						  		<h4 class="h-text"><a href="about.php?id=<?php echo $m['movie_id'];?>"><?php echo $m['movie_name'];?></a></h4>
						  		Cast:<Span class="color2"><?php echo $m['cast'];?></span><br>
						  		
						  	</div>
		  				</div>
		  		</div>
		  		
  	    <?php
  	    	}
  	    	?>
			
			</div>
				<div class="clear"></div>		
			</div>
			<?php include('footer.php');?>
profic
<?php include('header.php');
if(!isset($_SESSION['user']))
{
	header('location:login.php');
}
	$qry2=mysqli_query($con,"select * from tbl_movie where movie_id='".$_SESSION['movie']."'");
	$movie=mysqli_fetch_array($qry2);
	?>
<div class="content">
	<div class="wrap">
		<div class="content-top">
				<div class="section group">
					<div class="about span_1_of_2">	
						<h3 style="color:black;" class="text-center">BOOKING HISTORY</h3>
						<?php include('msgbox.php');?>
						<?php
				$bk=mysqli_query($con,"select * from tbl_bookings where user_id='".$_SESSION['user']."'");
				if(mysqli_num_rows($bk))
				{
					?>
					<table class="table table-bordered">
						<thead>
						<th>Booking Id</th>
						<th>Movie</th>
						<th>Theatre</th>
						<th>Screen</th>
						<th>Show</th>
						<th>Seats</th>
						<th>Amount</th>
						<th>admin</th>
						</thead>
						<tbody>
						<?php
						while($bkg=mysqli_fetch_array($bk))
						{
							$m=mysqli_query($con,"select * from tbl_movie where movie_id=(select movie_id from tbl_shows where s_id='".$bkg['show_id']."')");
							$mov=mysqli_fetch_array($m);
							$s=mysqli_query($con,"select * from tbl_screens where screen_id='".$bkg['screen_id']."'");
							$srn=mysqli_fetch_array($s);
							$tt=mysqli_query($con,"select * from tbl_theatre where id='".$bkg['t_id']."'");
							$thr=mysqli_fetch_array($tt);
							$st=mysqli_query($con,"select * from tbl_show_time where st_id=(select st_id from tbl_shows where s_id='".$bkg['show_id']."')");
							$stm=mysqli_fetch_array($st);
							?>
							<tr>
								<td>
									<?php echo $bkg['ticket_id'];?>
								</td>
								<td>
									<?php echo $mov['movie_name'];?>
								</td>
								<td>
									<?php echo $thr['name'];?>
								</td>
								<td>
									<?php echo $srn['screen_name'];?>
								</td>
								<td>
									<?php echo $stm['name'];?>
								</td>
								<td>
									<?php echo $bkg['no_seats'];?>
								</td>
								<td>
									Rs. <?php echo $bkg['amount'];?>
								</td>
								<td>
									<?php  if($bkg['ticket_date']<date('Y-m-d'))
									{
										?>
										<i class="glyphicon glyphicon-ok"></i>
										<?php
									}
									else
									{?>
									<a href="cancel.php?id=<?php echo $bkg['book_id'];?>" style="text-decoration:none; color:red;">Cancel</a>
									<?php
									}
									?>
								</td>
							</tr>
							<?php
						}
						?></tbody>
					</table>
					<?php
				}
				else
				{
					?>
					<h3 style="color:red;" class="text-center">Booking sucessfull</h3>
					<p>Once you start booking movie tickets with this account, you'll be able to see all the booking history.</p>
					<?php
				}
				?>
					</div>			
				<?php include('movie_sidebar.php');?>
				
			</div>
				<div class="clear"></div>		
			</div>
	</div>
</div>
<?php include('footer.php');?>
<script type="text/javascript">
	$('#seats').change(function(){
		var charge=<?php echo $screen['charge'];?>;
		amount=charge*$(this).val();
		$('#amount').html("Rs "+amount);
		$('#hm').val(amount);
	});
</script>





      

