<?php

$argv = $_SERVER['argv'];

if(isset($argv)) $tamanho = explode('x', $argv[1]);

if(isset($tamanho[1])){
  $terminalX = $tamanho[0] - 1;
  $terminalY = $tamanho[1] - 2;
} else {
  $terminalX = 79;
  $terminalY = 24;
}

if(isset($argv[2])){
  $imagemnome = $argv[2];
} else{
  $imagemnome = "apple.jpg";
}

$formato = explode('.', $imagemnome);
$formato = $formato[count($formato) - 1];

if($formato == 'jpg' OR $formato == 'jpeg'){
  $imagem = imagecreatefromjpeg($imagemnome);
} elseif($formato == 'png'){
  $imagem = imagecreatefrompng($imagemnome);
}

$nova = imagecreatetruecolor($terminalX, $terminalY);

$tamanhoX = imagesX($imagem);
$tamanhoY = imagesY($imagem);

imagecopyresampled($nova, $imagem, 0, 0, 0, 0, $terminalX, $terminalY, $tamanhoX, $tamanhoY);

for($y = 0;$y <= $terminalY; $y++){
  if($argv[3] == '-s'){
    usleep(100000);
  }
  for($x = 0;$x <= $terminalX; $x++){

		$rgb = imagecolorat($nova, $x, $y);
		$rgb = imagecolorsforindex($nova, $rgb);
		$r = $rgb['red'] * 1.0;
		$g = $rgb['green'] * 1.0;
		$b = $rgb['blue'] * 1.0;
		
		if(($r + $g + $b) < 100){
		  //Preto
		  echo "\033[30mA"."\033[0m";
		} elseif(($r + $g + $b) > 650){
		  //Branco
		  echo "\033[0m1";
		} elseif(($r == $b AND $b == $g)){
		  //Cinza
		  echo "\033[90m0";
		} elseif(($r > $g) AND ($r > $b)){
		  if($g > 170){
		    //Amarelo
  		  echo "\033[93mY";
		  } elseif($b > 130){
		     //Roxo
		     echo "\033[95mB";
		  } else {
		    //Vermelho
  		  echo "\033[91mR";
		  }
		} elseif(($g > $r) AND ($g > $b)){
		  if($r > 190){
		    //Amarelo
  		  echo "\033[93mY";
		  } elseif($b > 200){
		    //Azul Claro
		    echo "\033[96mG";
		  } else {
		    //Verde
  		  echo "\033[92mG";
		  }
		} elseif(($b > $r) AND ($b > $g)){
		  if($g > 190){
		    //Azul Claro
		    echo "\033[96mG";
		  } elseif($r > 130){
		    //Roxo
		    echo "\033[95mB";
		  } else {
		    //Azul
  		  echo "\033[94mB";
		  }
		} else {
		  echo "\033[90m0";
		}

  }
}

ob_start();
imagejpeg($nova);
$i = ob_get_clean(); 
$fp = fopen ('renderizada.jpg','w');
fwrite ($fp, $i);
fclose ($fp);

echo "\n\033[0m";

?>