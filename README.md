# Error Handling

Vi skal forbedre hackathon templaten så den bedre kan håndtere fejl og give ordentlige beskeder, der kan bruges til at debugge.
Error handling er vigtigt både for programmøren bag programmet, men også for brugerne, så de selv kan troubleshoot deres problemer.
# Error Handling i Endpoints
Kig på jeres endpoints. Lige nu står der noget i stil med:

return Response.status(200).type(MediaType.APPLICATION_JSON).entity(out).build();

Denne linje kode sender status 200 ud ligegyldig hvad jeres 'out' variabel indeholder. Status 200 betyder at koden er kørt uden problemer, men i tilfælde af f.eks. at customer-objektet ved en fejl bliver hentet som null, burde den jo ikke give status 200.

Prøv at lave et if-else statement, der returnerer status 400 i stedet med en tilsvarende fejlbesked, i tilfælde af:
1. Get customers returnerer null
2. Get customer returnerer null
3. Create customer kunne ikke oprette en bruger
4. Update customer kunne ikke opdatere brugeren

Eksempel på hvordan man returnerer fejl 400:
return Response.status(400).entity("Could not find customer").build();

Prøv at slå op på nettet hvad de forskellige fejlkoder betyder (e.g. 200, 400, 404, 500).

# Error Handling i Controller 
Lad os nu sige at vi har en bruger, der kommer til at indtaste en string i balance når personen prøver at oprette en bruger. Dette ville programmet heller ikke kunne klare, da den prøver at parse inputtet til en integer.

Hvis nu brugeren gjorde det ved et uheld, burde de nok få en chance til. Prøv, ved hjælp af en try-catch, at fortælle brugeres at de har et invalid input og de skal prøve med en integer, hvis de prøver at indsætte en bogstaver i balancen.

# Error Handling i database 
I database controlleren er der en query-metode. I tilfælde af den henter et tomt resultset ned, vil den stadig sende dette resultset videre. Lav en error handling der sørger for at printe en fejlbesked der fortæller listen er tom.

Sørg også for at sende en fejlbesked i tilfælde af der ikke kan oprette forbindelse til databasen. 
