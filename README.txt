Objašnjenje stilova i parametara koji utiču na parallax efekat
--------------------------------------------------------------

// perspective: 1px; definiše perspektivu od 1px. Svi layeri će imati z vrednost od 0 do 1. Što je z vrednost layera bliža 1, to je layer bliži korisniku, odnosno veći je i brže se pomera na scroll.
// position: relative; Position je relative jer će layeri imati position absolute.
.page {
    height: 100vh;
    perspective: 1px; 
    perspective-origin: center center;
    position: relative;
}

//transform-style: preserve-3d; Bez ovoga ne može
#parallax {
    transform-style: preserve-3d; 
    height: 100vh;
}

// .layer definiše zajedničke vrednosti za sve layere (mada su neke vrednosti override-ovane kasnije kao npr. background-position i background-size)
// top, right, bottom, left treba da bude postavljeno na 0.
.layer {
    background-position: bottom center;
    background-size: cover;
    background-repeat: no-repeat;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
}

// Prvi layer je Venom na kamenju. Najbliži je korisniku. Zato u translate3d stoji z vrednost od 0.6px. Svi ostali layeri imaju manju z vrednost od ove. 
// Takođe je background-size: cover jer treba da prekriva ceo ekran. Podrazumeva se da su neki delovi layera transparentni inače se ništa u pozadini ne bi videlo.
// Transformacija translate3d po x osi je 0, po y osi je -45px da bi se malo podigao layer i po z osi je 0.6. Vrednost z ose ne sme biti veća od 1 jer je u stilu .page perspective: 1px.
// scale sam podešavao proizvoljno.
#layer-1 {
    background-image: url('images/layer01.png');
    transform: translate3d(0, -45px, .6px) scale(.5);
    background-size: cover;
}

// Layeri 2, 3, 4 i 5 predstavljaju planete koje se vide iza Venoma. Zato je background-size: auto, jer ne moraju da prekrivaju ceo ekran, samo delove. Svi imaju z vrednost manju od 0.6px, jer najbliži layer ima tu vrednost.
// background-position je za neke left, a za druge right, u zavisnosti sa koje strane ekrana sam želeo da lociram određenu planetu.
#layer-2 {
    background-image: url('images/layer02.png');
    transform: translate3d(0, -50px, .2px) scale(.5);
    background-position: center left;
    background-size: auto;
}

#layer-3 {
    background-image: url('images/layer03.png');
    transform: translate3d(0, -180px, .45px) scale(0.5);
    background-position: center right;
    background-size: auto;
}

#layer-4 {
    background-image: url('images/layer04.png');
    transform: translate3d(0, -120px, .25px) scale(.4);
    background-position: center right;
    background-size: auto;
}

#layer-5 {
    background-image: url('images/layer05.png');
    transform: translate3d(0, -50px, .139px) scale(.3);
    background-position: center right;
    background-size: auto;
}

// layer-99 je poslednji layer. Predstavlja pozadinu (svemir) i najviše je udaljen od korisnika.
// Mogao sam da ga podesim isto kao i prethodne layere, ali sam izbacio translate3d i postavio background-attachment na fixed. Na taj način poslednji layer se ne pomera uopšta na scroll već je fiksiran za pozadinu.

#layer-99 {
    background-image: url('images/layer99.jpg');
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
}