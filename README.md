# cropping-image-in-php
# cropimage saving in folder and updating in db
        list($width, $height) = getimagesize($_FILES['sub_cat_img']['tmp_name']);
        if ($width < "1200" || $height < "750") {
            echo "<script>alert('Image dimension should be greater than   1200X750');</script>";
            return false;
        }
        if (($_FILES["sub_cat_img"]["size"] > 2000000)) {
            echo "<script>alert('Image size exceeds 2MB');</script>";
            return false;
        }
        if (!empty($_FILES['sub_cat_img']['name'])) {
            $file = $_FILES['sub_cat_img']['tmp_name'];
# crop image making part
            $save = "uploads/subcategory/" . $_FILES['sub_cat_img']['name'];   //This is the new file you saving
            
            $modwidth = 600;                                                   // width size for cropping
            $modheight = 400;                                                  // height size for cropping
            $tn = imagecreatetruecolor($modwidth, $modheight);
            $image = imagecreatefromjpeg($file);
            imagecopyresampled($tn, $image, 0, 0, 0, 0, $modwidth, $modheight, $width, $height);
            imagejpeg($tn, $save, 100);
 # crop image making end 

            $cat_img = "subcategory/" . $_FILES['sub_cat_img']['name'];
        } else {
            $cat_img = '';
        }
           $this->model->insert( $cat_img);
 # cropimage saving and updating in db end
