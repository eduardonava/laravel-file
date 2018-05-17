   public function save(Request $request)
	{
		$imagePath =  $_FILES['upload_file']['tmp_name'];
		$name =  $_FILES['upload_file']['name'];
		$resultado = "";
		$target_dir = "/home/eduardo/";
		$target_file = $target_dir . basename($_FILES["upload_file"]["name"]);
		$imageFileType = strtolower(pathinfo($target_file,PATHINFO_EXTENSION));

		if (move_uploaded_file($_FILES["upload_file"]["tmp_name"], $target_file)) {
	        $resultado = "The file ". basename( $_FILES["upload_file"]["name"]). " has been uploaded.";
	    } else {
	        $resultado =  "Sorry, there was an error uploading your file.";
	    }
		
		return view('lalo.index')->with(['resultado'=> $resultado]);
			    
	}
  
  <form action="{{ route('books.store') }}" method="POST" enctype="multipart/form-data">
    {{ csrf_field() }}
    <label for="upload_file" class="control-label col-sm-3">Upload File</label>
     <div class="col-sm-9">
          <input class="form-control" type="file" name="upload_file" id="upload_file">
     </div>
    <input type="submit" value=" Save " />

    <?php echo $resultado; ?>
</form>
