homework01
==========
<?php
mb_internal_encoding('UTF-8');
$pageTitle='Добавяне на разход';
include 'includes/header.php';

if($_POST){
    $name=  trim($_POST['name']);
    str_replace('/','', $name);
    $suma=trim($_POST['suma']);
    $suma = (float) str_replace(',','.', $suma);
    $selectedGroups=(int)$_POST['groups'];
    $date=date("d.m.y");
    $error=false;
    if(mb_strlen($name)<3){
        echo '<p>Името е прекалено късо</p>';
        $error=true;
    }
    if($suma<=0){
        echo '<p>Невалидна сума</p>';
         $error=true;
    }
    if(!array_key_exists($selectedGroups, $groups)){
        echo '<p>Невалидна група</p>';
         $error=true;
    }
    if(!$error){
        $result=$date.'/'.$name.'/'.$suma.'/'.$selectedGroups."\n";
        file_put_contents('data.txt', $result,FILE_APPEND);
    }
}
?>
        <a href="index.php">Списък разходи</a>
        <form method="POST">
            <div>Име:<input type="text" name="name"/></div>
            <div>Сума:<input type="text" name="suma"/></div>
            <div>Вид:
                <select name="groups">
                    <?php
                    foreach ($groups as $key=>$value) {
                        echo '<option value="'.$key.'">'.$value.'</option>';
                        
                    }
                    ?>
            </div>
                 </select>
        <div><input type="submit" value="Въведи"/></div>
        </form>
 <?php
include 'includes/footer.php';
?>

