	 work# Test

# Simulation
In order to always have simulation mode in panel pc:
$cd /opt/pst/etc
$touch tests

In order to use Automate Simulator:
configure hardware
$rm build_develop
$rm install_develop
$pst-tool build mistralplus_1.4
$cd workspace/install-develop/opt/pst/etc/
$mkdir virt
$cd virt
$touch errors  fs3  gui  nca  ncb  opcua  plc  profilometer  sortingengine  statistics
$pst-tool build plc_proxy (plc_proxy is responsible for starting the pipeline)
$cd workspace/install-develop/opt/pst/scripts/
Reset database, launch start_plc_proxy, ErrorServer, PlcServer, AutomateSimulator, PipelineServicesTool

## User Story
FFA : Fiche Fonctionnelle Applicative
3 amigos : Dev + Test + PO + eventuellement les parties prenantes

US Anomaly = lié directement au critère d'acceptation
Ticket Improvement/Amélioration = comme l'histoire du rejeu

## VPN
sudo openvpn --config PellencST.ovpn

## Pst Tool
* Show all machine modules :
pst-tool module list -m melanie

-  pst-tool --branch=branchname checkout tagname -> checks out tag from branchname
	pst-tool checkout tagname   ->  checks out tag from develop

Steps to do :

		def checkoutTag(branch_name, tag_name) -> None:
			cd git-branchname
			for dep in deps 
				out = git checkout branch_name
				if (!out)
					git fetch --all --tags
					out = git tag -l tag_name
					if (!out)
						git checkout tags/tag_name -b branch_name
					else
						print(this dep doesn't have %s (tag_name), working directory will be attached to HEAD)
				else:
					print(out.error)
	def main:
		#get all branches from web service
		if os.path.exists(os.path.join(workspace, "git-%s" % (args.branch)))
		if args.branch:
			if args.branch == 'all'
				for n in branchnames[]
					gitCheckoutTag(n, tag_name)
			elif os.path.exists(os.path.join(workspace, "git-%s" % (args.branch))):
				gitCheckoutTag(args.branch, tag_name)
			else:
		else:
			
			


pst-tool checkout tagname

*  pst-tool --branch=release clone mistralplus_1.4
	pst-tool --branch=release build mistralplus_1.4
	pst-tool --branch=release clone StatisticsServer
	pst-tool --branch=release build StatisticsServer

* pst-tool apps clone
* pst-tool module update all

- pst-tool checkout tagname
_____
- pst-tool build -c'-DPST_ENABLE_CPP17=ON' mistralplus_2.1
-c : passer un paramètre à CMake.

- 

## Things to put in place 
- The possibility to debug a unit_test with google test (from FIS)
- The encryption/decryption of SQLite data (from ACTIA)
- The possibility to retrieve data from different MySQL Data Servers at the same time. using ThreadPools. (from DS)

## PLC Errors
Les vrais erreurs qui viennent de l'automate sont les erreurs comme 52614 :
Envoyée à l'automate : false


25006 erreur modbus

mysqldump -upellencst -pmordor18 --all-databases > dump.sql

## Versions control
When we have already released a 4.8.0 stable, and for instance we have 4.8.0 RC 18 to be the last release version and we gave it to the client. One day, there was an anomaly in the latter version, so we fixed it for the client. In this case, we cannot do a 4.8.0 RC19, because the 4.8.0 stable was released. It will be a 4.9.0 RC1. In some cases, it's illogical to put the changes in the 4.9.0 RC1 because it won't have all the previous changes of the 4.8.0 Release branch.

la vecto c'est dans la 4.8.1


def gitCheckoutTag(directory: str, tag_name: str, branch_name: Optional[str]=None) -> None:

print('\nGit checkout tag ...')

if os.path.exists(directory):

subprocess.run("git fetch --all --tags", shell=True, stdout=subprocess.PIPE, stderr=subprocess.DEVNULL, cwd=directory)

if branch_name:

subprocess.run("git checkout tags/%s -b %s" % (tag_name, branch_name), shell=True, stdout=subprocess.PIPE, stderr=subprocess.DEVNULL, cwd=directory)

else:

  

#git-develop

#git-release

#git-stable

#git-vecto

  

else:

print('Path %s does not exist' % (directory))


machine 
brick
module 
apps
clone
build
-clean
-test
-test-asan
-test-tsan
cppcheck
doxygen
sonar
build-package
clean-package
build-cfast
checkout

# Machine IP Address fixe 
- 10.4.90.11 pour la TO1 (connect)
- 10.4.90.21 pour la TO2 (compact)
- 10.4.90.31 pour la TO3 (watemark)
- 10.4.90.41 pour la TO4 (R&D)
- 10.4.90.51 pour la TO5 (qc)
- 10.4.90.61 pour la TO6 (trium)

# Tests

Avant de partir en vacance, j'ai terminé un ticket et j'ai demandé à Aziza si son test est déjà fait, pour que je fasse son test d'intégration, elle m'a dit que oui c'est déjà fait. Alors, j'ai commencé à travailler sur un nouveau ticket et j'ai vu que son test n'est toujours pas créé donc j'ai créé son ticket, je m’y suis assigné, et j'annonce dans le daily que je vais m'occuper de ce test. En revenant des vacances, je voix qu'elle a commencé à faire le travail que je suis supposé de faire, et quand je lui ai parlé pour avoir des explications, elle m'a dit que j'étais en vacances, et que c’est son travail et c'est elle qui s’occupe des tests et si je veux je pourrais parler à Arnaud. Pourtant, elle n'a pas fait d'objection quand j'ai dit que je vais prendre le ticket avant les vacances. Qu'est ce qu'on appelle ça ? monopolisation des tests ? Moi au début j'ai dit que je veux travailler dans tout le cycle de vie du développement logiciel, et Olivier confirme aussi que les développeurs doivent faire des tests unitaires. 

L'étrange dans l'histoire, c'est que c'est elle qui a dit qu'il faut créer un ticket avant de modifier dans les tests, et maintenant elle fait ça ?

____
I noticed when I get the parent of a family, it returns the "Objects" FolderType Node::Id, which is wrong, it should return the object of type FamiliesProviderType Node::Id.

BUG : Parent Id changes after calling AddNode from client
-> I CANNOT DELETE ISSUES https://pellencst.atlassian.net/browse/LEO-167

- When you give a node Id in a parameter and try to access it's opc-ua variables like NAME or PARENT or ID, it will not understand it. You need to search for it first.

- we cannot change Node::NAME & Node::DISPLAY_NAME when we rename our family -> so we need to create a variable to save the name.

- Réunion lundi matin pour ajouter les modifications dans le modèle.
- Changement de couleur sans request ( directement dans le serveur )
- créer réunion avec Olivier Aubert
- How to call  changeDisplayName in the controller? 
- Record to say that Channels have been deleted.
- Record to say that Channels have been created.

- ON_SCOPE pour la suppression de la configuration de famille
- ChannelCountChangeEventRecordType

PST_EXCEPTION_THROW_IF ( find ( inName ) != end(), ErrorCode::DuplicateProperty, "Duplicate property ", inName );

# SN3 dans Orchestra
Support SLC ou SCL ou LSC.....