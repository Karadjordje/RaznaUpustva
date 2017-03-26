Sta sve treba instalirati za koriscenje yeoman-a (https://github.com/yeoman/generator-webapp)

1. Git bash
2. Source tree
3. Node.js
4. Gulp
5. Ruby
6. Python

Kako koristis:
Udjes u source tree ides clone/new i kopiras sa githab-a (napravis repozitorum tamo) link
Onda ukljucis git bash u folderu gde radis i kucas sledece (getting startet upustvo preuzeto sa https://github.com/yeoman/generator-webapp):

npm install --global yo gulp-cli bower generator-webapp
yo webapp (Ovde cepas samo Enter kad se pojavi cikica neki)
gulp serve (Da vidis/gledas promene)
bower install --save <package>  (ime paketa koji oces da isntaliras)
gulp (kad oces da izgradis projekat)
Jos neke komande:
gulp serve:test (za testiranje u browser-u)
gulp serve:dist (za pregled produkcije)
ctrl c (prekidas procese)

Kad nastavljas da radis samo udjes u folder otvoris gitbash i kucas gulp serve
Kad oces da instaliras neki jq pluggin kucas bower install i on ce ti se pojaviti u bower folderu i ti jos treba da dodas link u indexu (yeoman to sam radi, ali zna da baguje)

Kako se radi u njemu (SASS): 
1. Imas main scss: u njemu kucas recimo @import header (gde je header ID iz index.html-a). Na taj ubacujes delice scss-a u main gde se sklapaju.
2. Kad pravis scss fajl dodajes mu ispred imena _   (Napomena: ovo vazi za svaki fajl sem main.scss fajla, kad ga pozivas u main.scss pozivas bez _ )

Primer main.scss:

$icon-font-path: '../fonts/';

	// bower:scss
	@import "bower_components/bootstrap-sass/assets/stylesheets/_bootstrap.scss";
	// endbower


	@import "colors";
	@import "nav";
	@import "ourLogo";
	@import "pokemons";
	@import "footer";
	@import "modalSection";

	// Add color for body, color classes in colors.scss
	body {
	  background-color: $body;
	  font-family: 'PT Serif', serif;
	}

Primer fajla koji nije main.scss:

	#questions {
		background-color: #fff;
		margin-top: 4em;
		ol {
	    	text-align: center; 
	    	list-style-position:inside;
	    	padding: 0em;
		}
		li {
			font-size: 1.5em;
			margin-top: 0.3em;
		}
	}


Kad odradis nesto: 
Ides u source tree i tamo ides stage all > zatim comit (proporocujem da dodas komentar da znas sta si radio) > zatim push > to je to

Za instaliranje font awesome:  Obe ne rade jer je yoaman ubagovan > brzo resenje dodaj cdn u head
Kucaj ovo u gitbas: bower install components-font-awesome --save
                    bower install --save fontawesome


Ovo nije vezano za yeoman direktno ali tako sam brisao foldere gde sam koristio yeoman > Kad brises fajlove napravis text file >delete.txt ubacis sl.text u njega:

SET DIRECTORY_NAME="D:\Projekti programiranje\Test"
TAKEOWN /f %DIRECTORY_NAME% /r /d y
ICACLS %DIRECTORY_NAME% /grant administrators:F /t
PAUSE

Menjas samo path odnosto directory name kad to namestis promenis ime fajla u delete.bat i pokrenes ga > izbrises folder