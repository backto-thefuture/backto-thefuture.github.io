# Workflow da Mesh a 3DHOP  
  
Giacomo - Alessandra ci inviano i modelli in formato .obj con texture .jpg e .mtl  
  
NOMETEMPIO_DX/SX_texture.obj  
NOMETEMPIO_DX/SX_texture.jpg  
NOMETEMPIO_DX/SX_texture.mtl  
  
Questi files vengono salvati nella cartella nometempio_original dentro la cartella nometempio_obj.  
  
la directory dei files è così strutturata:  
GitHub> nometempio>  
>nometempio_3dm per Mic e i files di annotazione in Rhino e Grasshopper  
>nometempio_img export immagini per annotazione Grasshopper  
>nometempio_mix files da meshmixer per il close cracks/chiusura modelli  
>nometempio_mpl files di meshLab  
>nometempio_nexus files compressi .nxs e .nxz ottenuti mediante processo Nexsus v. 4.2  
>nometempio_obj files grezzi poi elaborati in MeshLab  
>nometempio_ply files finali per compressione Nexsus v. 4.2    
  
Elisabetta apre il file in MeshLab e ottimizza il modello per il visualizzatore 3DHOP  
  
**1. aprire una nuova sessione di MeshLab**  
  
File > Import Mesh  
Filters > Normals, Curvatures and Orientation> Transform:Scale, Normalize > Uniform Scaling [100] Freze Matrix > Apply > Close (questo perchè 3DHOP lavora con unità pari a 1 - i modelli arrivano scalati in m, noi li vogliamo in cm)
Filters > Normals, Curvatures and Orientation> Transform:Translate, Center, set Origin > Transformation:Center on BBox > Apply > Close  
File > Export Mesh As.. > DX/SX_NOMETEMPIO.obj nella cartella nometempio_obj
  
**2. aprire una nuova sessione di MeshLab**  
  
File > Import Mesh > DX/SX_NOMETEMPIO.obj  
Filters > Normals, Curvatures and Orientation > Transform:Translate, Center, set Origin > Posizionare il modello secondo la posizione desiderata  
considerare FOV: ca. 60 - la Y và flippata con la Z  
Filters > Mesh Layer > Matrix:Freeze Current Matrix  
Filters > Normals, Curvatures and Orientation> Matrix:Freeze Current Matrix  
File > Export Mesh As.. > DX/SX_NOMETEMPIOmesh.obj (tutte le spunte attive e rinomina texture con DX/SX_NOMETEMPIOmesh.jpg) nella cartella nometempio_obj  
File > Save Project As > nometempio.mlp nella cartella nometempio_mpl  
  
NB) Nel caso la nuova texture non venga riconosciuta, aprire con Atom o simile, tasto_dx> file .mtl e aggiungere .jpg o il nome completo del file utilizzato per la texture da associare (ultima riga di comando) "map_Kd DX/SX_NOMETEMPIOmesh.jpg"   
  
**3. aprire una nuova sessione di Meshmixer**  
  
Import > DX/SX_NOMETEMPIOmesh.obj  
File > Save > nometempio.mix nella cartella nometempio_mix  
(nel caso ci sia YZ invertite - File > Import > Replace - Flip Z-Y on Import/Export)  
Edit > Close Cracks  
Analysis > Inspector (verificare e risolvere eventuali problemi Mesh) > Done  
Edit > Plane Cut (Ritagliare le parti in eccesso del modello per chiudere la parte basamentale)  
Analysis > Inspector (chiudere la Mesh) > Done  
File > Export > DX/SX_NOMETEMPIOmeshmixer.obj nella cartella nometempio_mix  
  
NB) Meshmixer avrà creato altre texture aggiuntive per le nuove superfici di chiusura create e rispettivo nuovo file .mtl 
  
**4. aprire MeshLab**  
  
File > Open Project > nometempio.mlp  
File > Import Mesh > DX/SX_NOMETEMPIOmeshmixer.obj (mantenere questi layer attivi)  
Filters > Mesh Layer > Matrix:Freeze Current Matrix  
Filters > Normals, Curvatures and Orientation> Matrix:Freeze Current Matrix  
File > Export Mesh As.. > DX/SX_NOMETEMPIO.ply (mantenere attivo solo Wedge - TextCoord + Binary Encoding + All) > OK  
Salvare i files con estensione .ply nella cartella nometempio_ply e insieme copiare i files texture precedente creati da MeshMixer che si trovano nella cartella nometempio_mix (vedi punto 5)   
  
**5. Salvare il materiale relativo a .obj e texture nella cartella Github/nometempio_ply/**    
DX/SX_NOMETEMPIO.ply  
DX/SX_NOMETEMPIOmeshmixer.mtl  
DX/SX_NOMETEMPIOmeshmixer_material_0.jpg  
DX/SX_NOMETEMPIOmeshmixer_GeneratedMat1.jpg  
  
**6. Nexus_4.2 (dopo aver scaricato nexus e averlo un-zippato da qualche parte)**  
  
Copiare i file nella cartella un-zippata di Nexus:  
DX/SX_NOMETEMPIO.ply  
DX/SX_NOMETEMPIOmeshmixer.mtl  
DX/SX_NOMETEMPIOmeshmixer_material_0.jpg  
DX/SX_NOMETEMPIOmeshmixer_GeneratedMat1.jpg  
  
**6.1 Nexus_4.2 Creazione file .nxs**  
  
Aprire con Editor di Testo "Build_Nexus.bat" (tasto dx - Apri con..) e scrivere/riscrivere i comandi per la creazione del file .nxs  
  
nxsbuild DX_NOMETEMPIO.ply -o DX_NOMETEMPIO.nxs  
nxsbuild SX_NOMETEMPIO.ply -o SX_NOMETEMPIO.nxs  
(va bene anche una sola riga, fare una riga per ogni file che si vuole convertire)  
  
Salvare il file Build_Nexus.bat e chiudere l'Editor  
Doppio Click su Build_Nexus.bat (a questo punto apre in automato il cmd e fa quello che deve fare...)  
  
Dovrebbe apparire  
> Components: mesh textures  
> Normals enabled  
> Textures enabled  
> Creating level 0  
> ...  
  
Al termine, verificare che esita un file NOMETEMPIODX/SXmeshmixer.nxs sparso nella cartella Nexus_4.2 (ci mette un pò di tempo)  
  
**6.2 Nexus_4.2 Creazione file .nxz**  
  
Aprire con Editor di Testo "Compress_Nexus.bat" (tasto dx - Apri con..) e scrivere/riscrivere i comandi per la creazione del file .nxz  
    
nxscompress DX_NOMETEMPIO.nxs -o DX_NOMETEMPIO.nxz  
nxscompress SX_NOMETEMPIO.nxs -o SX_NOMETEMPIO.nxz  
(va bene anche una sola riga, fare una riga per ogni file che si vuole convertire)  
  
Salvare il file Compress_Nexus.bat e chiudere l'Editor  
Doppio Click su Compress_Nexus.bat (a questo punto apre in automato il cmd e fa quello che deve fare...)  
  
Dovrebbe apparire (i numeri variano)  
  
> Vertex quantization step: 0.000  
> Texture quantization step: 0.25  
> Saving with flag: 4 (compressed with CORTO)  
> Textures: 117   
  
Al termine, verificare che esita un file NOMETEMPIODX/SXmeshmixer.nxz sparso nella cartella Nexus_4.2 (ci mette poco tempo)  
  
_ . _ . _ . _ . _  
  
*A questo punto i file .nxz possono essere richiamati dalle loro directory mediante codice html e sono visualizzabili online :)*
