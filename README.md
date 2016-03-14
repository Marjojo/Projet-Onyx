# Projet-Onyx

<?php
	session_start();
	$hostname = "localhost";
	$user = 'root';
	$passwd = '';
	$nomBase = 'tuttest';
	try {
		$connexion = new PDO('mysql:host='.$hostname.';dbname='.$nomBase, $user, $passwd);
	}
	catch (Exeption $e){
		die('Erreur : '.$e->getMessage());
	}
	try {
		$sql = $connexion->prepare('SELECT * FROM joueur WHERE prenom = :prenom AND email = :email');
		$sql->execute(array('prenom' => $_SESSION['prenom'], 'email' => $_SESSION['email']));
	}
	catch (Exeption $e){
		die('Erreur : '.$e->getMessage());
	}
		
	$data = $sql->fetch();
?>
<!DOCTYPE html>
<html lang="fr">
	<head>
		<meta charset="UTF-8">
		<title>Jeu Onyx</title>
		<meta http-equiv="x-ua-compatible" content="ie=edge">
	    <meta name="viewport" content="width=device-width, initial-scale=1">

	    <meta name="description" content=""/>
		<meta name="keywords" content=""/>
		
		<link rel="stylesheet" type="text/css" href="css/main.css">
		<link rel="stylesheet" type="text/css" href="css/jeu.css">
	</head>
<body>
		<!-- <aside>
			<div class="menuOnyx">
				<div class="retourInscrip">
					<a href="index.php"><img src="img/logos/onyx.png"></a><a href="index.php">Retour inscription</a>
				</div>
				<div class="chapitre">
					CHAPITRE 4 - Un nouvel espoir...
				</div>
			</div>
		</aside> -->
		<?php
			include('menu.php');
		?>
		<article>
			<!-- <audio src="musique.mp3" loop autoplay></audio> -->

			<?php if($data[3] == 1){$style = 'block';}else{$style = 'none';}?>
			<section class="intro" style="display: <?php echo $style ?>;">
					<div class="item">
						<h2>Début du jeu</h2>
						<p>Bonjour <b><?php echo $_SESSION['prenom'] ?></b>, pour avancer dans l'histoire, cliquez sur la flèche.</p>
						<div class="next">
							<img src="img/fleche.png" class="fleche-next">
						</div>
					</div>
					<div class="item hidden">
						<p>Seb et ses fameux mails d’urgences la dernière fois c’était pour se plaindre des retards des employés</p>
						<div class="next">
							<img src="img/fleche.png" class="fleche-next">
						</div>
					</div>
					<div class="item hidden">
						<p>Chéri le diner est prêt !</p>
						<div class="next suite">
							<img src="img/fleche.png" class="fleche-next">
						</div>
					</div>
			</section>

			<?php if($data[3] == 2){$style = 'block';}else{$style = 'none';}?>
			<section class="slide1" style="display:<?php echo $style ?>;">
					<div class="item">
						<p>Aujourd'hui j'ai vu Simone, elle a encore grossi. Tu te rends compte qu'à l'époque elle attirait tout les hommes, quand même il y a des gens qui ...</p>
						<div class="next">
							<img src="img/fleche.png" class="fleche-next">
						</div>
					</div>
                    <div class="item">
						<p><i>Tiens il me semble avoir entendu Onyx à la télé...</i></p>
						<div class="next">
							<img src="img/fleche.png" class="fleche-next">
						</div>
					</div>
					<div class="item hidden">
						<p>Désirez-vous augmenter le volume de la télévision ?</p>
						<button type="button" onclick="suite(1)">Oui</button>
						<button type="button" onclick="suite(2)">Non</button>
					</div>
                <!--//s'il clique sur non-->
					<div class="item hidden">
						<p>Non c'est encore un reportage inutile, je préfère ne pas écouter de telles sottises  pendant mon jour de repos</p>
						<div class="next">
							<img src="img/fleche.png" class="fleche-next">
						</div>
					</div>
			</section>

			<?php if($data[3] == 3){$style = 'block';}else{$style = 'none';}?>
			<section class="slide2" style="display:<?php echo $style ?>">
				<div class="item">
					<p>La société multinationale d'élevage de bovins Onyx dirigée par Sébastien Baros et son associé <?php $_SESSION['prenom'] ?> vient d'acquérir de nouvelles terres en Amazonie. Cependant ce n'est pas la première fois qu'Onyx est sujet à controverse, les associations écologiques s'opposent encore à cet achat par crainte de déforestation massive. Pour contrer l'entreprise, une demande de label vert par les associations a été demandé au gouvernement brésilien. Si jamais ce label est accepté, l'entreprise pourrait perdre son terrain.
					<i>Vous voulez en savoir plus sur le label vert ? <a href="#">Lien vers youtube</a></i></p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
			</section>

			<?php if($data[3] == 5){$style = 'block';}else{$style = 'none';}?>
			<section class="slide3" style="display:<?php echo $style ?>">
				<div class="item">
					<p>C'est Sébastien, qu'est ce qu'il peut bien vouloir à une heure pareille ?</p>
                    <div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
                <div class="item hidden">
						<p>Voulez vous répondre à Sebastien ?</p>
						<div class="next">
							<button type="button" onclick="suite(3)">Répondre</button>
					<button type="button" onclick="suite(4)">Ignorer l'appel</button>
						</div>
					</div>
                </section>
            <!--Si oui-->
            <?php if($data[3] == 5){$style = 'block';}else{$style = 'none';}?>
			<section class="slide5" style="display:<?php echo $style ?>">
				<div class="item hidden">
					<p>Allo <?php $_SESSION['prenom'] ?> ? C'est Sébastien ! Pourtquoi tu ne réponds pas ? Je t'ai laissé plusieurs messages et même un mail ! Il faut que tu viennes au bureau maintenant car... Je ne peux rien te dire au téléphone. Viens je t'expliquerai tout sur place.</p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
            </section>
            <!--si non-->
            <?php if($data[3] == 5){$style = 'block';}else{$style = 'none';}?>
			<section class="slide4" style="display:<?php echo $style ?>">
				<div class="item hidden">
					<p>Ah non pas ce soir ! Sébastien peut bien attendre, pour une fois que je suis à la maison.</p>
					<div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
            </section>
			
            <!--Sil a répondu à l'appel de Seb-->
			 <section class="slide6">
				<div class="item">
					<p>Sébastien est vraiment sérieux cette fois-ci. C'est la première fois que je l'entends aussi inquiet. Il y a bien eu la fois où au dernier moment nous avons perdu un client, mais là... Quelque chose d'important à du se produire.</p>
					<div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
			</section>

			<section class="slide7">
				<div class="item">
					<p><i>Sébastien qu'est ce qui ce passe ? J'ai fais aussi vite que j'ai pu !</i></p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
				<div class="item hidden">
					<p>Tu as vu les infos ? On parle de nous et de notre situation. Déjà que l'entreprise est mal en point... Nos demandes en cuir sont de plus en plus fortes, ils nous faut plus de terrain pour élever les bovins. Nous avons besoin de ce terrain en Amazonie par n'importe quels moyens ! Avec cette affaire, les médias ne nous lâche plus... On avait franchement pas besoin de ça !</p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
				<div class="item hidden">
					<p>Calme toi... Sur la vente du terrain nous sommes prioritaire non ? On avait réglé les derniers détails.</p>
					<div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
			</section>

			<section class="slide8">
				<div class="item">
					<p>Seb: Je t'ai envoyé un mail ! Avec le label vert, les autorités vont commancer à surveiller nos activités on ne peut pas se permettre une erreur sinon on risque la perte de ce terrain. Il faut détruire certains éléments qui pourraient nous compromettre. Et ces associations d'hippies s'annonçant sois disant protectrices des droits de l'homme qui ne nous lâchent pas ! Rien ne va plus ! J'ai fait appel à une de mes connaissances il m'a proposé une alternative... Elle serait efficace mais cela doit rester secret. Il n'y a qu'à toi que je fais confiance.</p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
				<div class="item hidden">
					<p>Seb attends... De quoi parles-tu ? Une solution alternative ? Tu ne m'en a jamais parlé, tu devais me consulter avant d'exposer notre problème à un inconnu, je ne sais pas qui c'est !</p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
				<div class="item hidden">
					<p>Il fallait réagir ! Tu n'étais pas disponible, je n'avais pas le choix. Je devais me tourner vers quelqu'un pour trouver une solution. Il est avocat, fais moi confiance, il peut nous aider !</p>
					<div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
                <div class="item hidden">
					<p>Voulez vous écouter la proposition de Sébastien ?</p>
					<button type="button" onclick="suite(6)">Oui</button>
					<button type="button" onclick="suite(7)">Non</button>
				</div>
			</section>

			<section class="slide9">
				
				<div class="item">
					<p>Les investisseurs nous mettent la pression, j'en ai parlé à mon ami et il m'a mis en relation avec quelques contacts. Il a une solution sur notre nouvelle acquisition en Amazonie. Prends leurs coordonnées, tu verras ce sont des professionnels, ils ont déjà eu à faire à ce genre de problèmes. Tu peux avoir confiance en eux. Je t'ai déjà pris ton billet d'avion et ton hotel est réservé. un chauffeur t'attends en bas, tu dois partir immédiatement.</p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
            </section>
            <section class="slide9"> <!--ajouter une autre photo-->
				<div class="item hidden">
					<p>Non tu devais m'en parler, comment peut-tu prendre des décisions pour l'entreprise tout seul ?!</p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
				<div class="item hidden">
					<p>Ecoute moi on a plus le choix, un de nous dois partir sur le terrain. Tu ne veux pas entendre la proposition très bien, mais tu sais très bien que je ne peux pas me déplacer pour le moment je dois rester pour calmer la presse ici et gérer l'entreprise. Tu es le meilleur pour gérer la situation là-bas. Un chauffeur t'attends en bas</p>
					<div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
            </section>
                    <!--Si oui pour écouter proposition Seb-->
            <section class="slide10"> <!--ajouter une autre photo-->
				<div class="item">
					<p>Qui sont ces contacts ?  Je me demande si je peux leur faire confiance ...</p>
					<div class="next">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
            </section>
            <section class="slide11">
            <!--Si non-->
				<div class="item">
					<p>Comment Sebastien a pu me faire ça ? Nous sommes associés, et il m’a tenu à l’écart. Je dois me débrouiller seul maintenant . Je verrais si j’ai besoin de son aide là-bas.</p>
					<div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
				</div>
            </section>
            <section class="slide12">
                    <div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
            </section>
            <section class="slide13">
                <div class="item">
					<p>Je vais pouvoir me reposer un peu.</p>
                    <div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
                </div>
            </section>
            <section class="slide14">
                <div class="item">
					<p>Voyons voir ce qu’il y a à la télé.</p>
                    <div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
                </div>
                <div class="item hidden">
					<p>Voulez vous voir le reportage ? Lien youtube</p>
                    <div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
                </div>
                <div class="item hidden">
					<p>Bon je dois me coucher, j’ai une réunion importante demain.</p>
                    <div class="next suite">
						<img src="img/fleche.png" class="fleche-next">
					</div>
                </div>
                
            </section>
			
		</article>
			
	<script type="text/javascript" src="http://code.jquery.com/jquery.js"></script>
	<script type="text/javascript" src="js/main.js"></script>
</body>
</html>
