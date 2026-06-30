---
tags:
  - paskaita/bioinformatika
  - programavimas/perl
created: 2026-02-04T08:30:00
Paskaita: Bioinformatika
LINKS:
---
Rekomenduotina nepraleisti testukų. 5 - laboratorianiai, 4 - egzaminas ir koliokviumas, 1 - skatinamieji, testukai, dalyvavimas. Atsikaitymai tik gyvai, vėluot negalima. **ATSISKAITYTI KUO ANKSČIAU**. Reikia rašyti tvarkingai, su komentarais ir normaliais pavadinimais. Galima naudotis bet kuo išskyrus AI. Mokysimės PERL????

```perl
#!/usr/bin/perl 

use strict;
use warnings;

```

## Perl 

- Aukšto lygio interpretuojama kalba
- Ilgalaikis stabilumas
- Plačiai naudojama *'*nix* sistemose
- Šveicariškas peiliukas - apjungia bash, sed, awk ir kitas pan. komandinės eilutės įrankių funkcionalumą.
- Istoriškai (buvo) paplitusi bioinformatikoje

```perl
#!/usr/bin/perl 

use strict;
use warnings;

print "Hello, World!\n";

```


```perl
#!/usr/bin/perl 
use strict; #neleidžia daryti tam tikrų nesaugių dalykų
use warnings; #%jungia papildomus ispejimus

my $greeting = 'Sveikas, pasauli!'; 

print $greeting, "\n";
```

"" - tekstas yra interpoliuojamas, '' - tekstas paimamas pažodžiui

Perl nereikia nustatyti tiesiogiai koks kintamojo tipas, naudojamas kontekstas. Perl kalboje yra vienas paprastas duomenų tipas - **skaliaras**. Galima suprasti kaip dėžutę, kurioje saugomas vienas dalykas. 

```perl
my $e = 'A'; 
my $f = 'B'; 
my $g = 3; 
my $h = 0.14; 
my $k = [ 1, 2, 3 ]; # čia nuoroda į vietą, kur yra saugomi elementai
my $m = \&sum; 
my $n = $e . $f; # 'AB' 
my $p = $g + $h; # 3.14 
my $r = 10 % 3; # 1 
my $s = '2' + 3; # $s == 5 
my $t = 'a' + 2; # $t == 2
```

Perl neturi teisingumo reikšmių ir boolean duomenų tipo. Viską priima kaip tiesa išskyrus kelias tam tikras reikšmes - 0, "", "0", undef.

```perl
my $x = 1; 
my $y; # kintamasis $y neapibr˙ežtas

defined $x # true 
defined $y # false

$x = undef; 
defined $x # false

print '$x == 5' if !($x - 5); 
print '$x yra lyginis' if !($x % 2);

print 'i˛vestis tušˇcia' if !(<>); 
print 'tušˇcias posekis' if !substr( 'hay', 2, 0 );

my $y; print '$y neapibr˙ežtas' if !$y
```

Masyvai nurodomi su @ simboliu. Naudojami paprasti skliaustai. Kai norima pasiekti elementą, naudojamas $.

```perl
my @e = ( 1, 2, 3 ); 
my @f = ( '1', '2', '3' ); 
my @g = ( 1, '2', 'a' );

$e[0]; # '1' 
$e[-1]; # '3' 
@f[0..2]; # '1', '2', '3' 
@f[0..0]; # '1' 
$f[3]; # undef

my @h = ( 'a', 'b', 'c' ); 
push( @h, 'd' ); # @h == ( 'a', 'b', 'c', 'd' ) 
my $k = pop( @h ); # $k == 'd'; @h = ( 'a', 'b', 'c' ) 
unshift( @h, 'x' ); # @h == ( 'x', 'a', 'b', 'c' ) 
my $m = shift( @h ); # $m == 'x'; @h = ( 'a', 'b', 'c' )
```

Asociatyvūs masyvai veikia kitaip. Inicijuojami su %, panašu į hash arba list. A -> B, C -> D. 

```perl
my %x = ( 'A' => 'T', 'C' => 'G' ); 
my %y = ( 'A', 'T', 'C', 'G' ); # kiek sunkiau skaitoma

my $f = $x{'A'} # $f == 'T' 
my $h = $y{'U'} # $h neapibrežtas (undef)

$x{'G'} = 'C';

delete( $x{'C'} );
```

```perl
my %hash = ( 'A' => 'T', 'Z' => 'X', 'Y' => 'W' ); 
$hash{'Y'} = undef; 
delete $hash{'Z'};

exists $hash{'A'} # true (raktas buvo priskirtas) 
exists $hash{'Z'} # false (raktas buvo ištrintas) 
exists $hash{'X'} # false (raktas nebuvo priskirtas) 
exists $hash{'Y'} # true (neapibr˙ežta tik reikšm˙e)

defined $hash{'A'} # true (reikšm˙e buvo priskirta) 
defined $hash{'Z'} # false (raktas buvo ištrintas) 
defined $hash{'X'} # false (raktas nebuvo priskirtas) 
defined $hash{'Y'} # false (buvo priskirta undef reikšme)
```

Priskyrimai:

```perl
my $e = 5;

my @f = ( 2, 4, 6 ); my $g = @f; # $g == 3 (masyvo dydis) 
my $h = scalar( @f ); # $h == 3 (masyvo dydis) 
my( $k ) = @f; # $k == 2 (pirmas @f elementas) 
my( $m, $n ) = @f; # $m == 2, $n == 4 
my( $p ) = scalar( @f ); # $p == 3 (masyvo dydis) 
my( undef, $r, $s ) = @f; # $r == 4, $s == 6

my %j = ( 'a' => 1, 'b' => 3 ); 
my $k = %j; # Rezultatas priklauso nuo Perl versijos 
my( $n ) = %j; # $n == kuris nors atsitiktinis raktas



my %x = ( 'A' => 1, 'B' => 2, 'C' => 3, 'D' => 4 ); 
my @z = %x; 
print "@z\n"; #B 2 D 4 A 1 C 3

my @g = ( 'A', 1, 'B', 2, 'C', 3 ); 
my %h = @g; 
use Data::Dumper; 
print Dumper( \%h );
#$VAR1 = { 'B' => 2, 'C' => 3, 'A' => 1 };


my %hash = ( 'a' => 1, 'b' => 3, 'd' => 7 ); 
print scalar %hash, "\n";
#3/8  asociatyvaus masyvo užpildymo duomenys iki Perl v5.26.0
#po to 3 asociatyvaus masyvo elementu˛ skaiˇcius. Tačiau tai prastina kodo portailumą

```

Keys funkcija grąžina asociatyvaus masyvo raktų sąrašą. Atvirkščiai, values grąžina  reikšmias.

```perl
my %h = ( 'A' => 'T', 'C' => 'G' );

my @g = keys %h; # @g == ( 'A', 'C' ) arba # @g == ( 'C', 'A' )

my @c = ( 'A', 'C', 'G', 'T' ); 
my @d = keys @c; # @d == ( 0, 1, 2, 3 ) 
for my $i (keys @c) { ... }
```

Geriau yra apsieiti be laikinų kintamųjų:

```perl
my @arrayOfKeys = keys %hash; 
for my $key ( @arrayOfKeys ) {
	 ... 
} 
my $numberOfKeys = scalar( @arrayOfKeys ); 
print $numberOfKeys;

for my $key ( keys %hash ) {
	... 
}

print scalar( keys %hash );
```

```perl
5 == 5; # true 
3 != 3; # false 
1 < '2'; # true 
'6' >= '10'; # false

'a' eq 'b'; # false 
'ac' ne 'dc'; # true 
'e' lt 'd' # false 
'f' ge '10'; # true
```

```perl
if( $condition_a ) { 
	print 'TRUE'; # patenkinta s ˛alyga $condition_a
} elsif( $condition_b ) { 
	print 'OTHER'; # patenkinta s ˛alyga $condition_b 
} else { 
	print 'FALSE'; # abi s ˛alygos nepatenkintos 
}

unless( $condition_c ) { ... } 
# Tas pats kaip: 
if( !$condition_c ) { ... }

print 'TRUE' if $boolean; 
print 'TRUE' unless $boolean;
```

```perl
for my $iterator (@elements) { print $iterator * 2 } 
for (@elements) { print $_ * 2 }

for my $i (1..10) { ... } 
for my $i (0..$#elements) { ... } # == 0..(@elements-1)

for ( my $i = 0; $i < 10; $i++ ) { ... } 
for ( my $i = 0; $i < @elements; $i++ ) { ... }

my $i = 0; 
while( $i < $n ) { ... $i++; }

for ( my $i = 0; $i < $n; $i++ ) { ... }
```