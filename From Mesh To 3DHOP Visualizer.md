# Workflow da Mesh a 3DHOP  
  
Giacomo - Alessandra ci inviano i modelli in formato .obj con texture .jpg e .mtl  
  
NOMETEMPIO_DX/SX_texture.obj  
NOMETEMPIO_DX/SX_texture.jpg  
NOMETEMPIO_DX/SX_texture.mtl  
  
Elisabetta apre il file in MeshLab e ottimizza il modello per il visualizzatore 3DHOP  
  
**1. aprire una nuova sessione di MeshLab**  
  
File > Import Mesh  
Filters > Normals, Curvatures and Orientation> Transform:Scale, Normalize > Uniform Scaling [100] Freze Matrix > Apply > Close (questo perchè 3DHOP lavora con unità pari a 1 - i modelli arrivano scalati in m, noi li vogliamo in cm)
Filters > Normals, Curvatures and Orientation> Transform:Translate, Center, set Origin > Transformation:Center on BBox > Apply > Close  
File > Export Mesh As.. > DX/SX_NOMETEMPIOmesh.obj  
  
**2. aprire una nuova sessione di MeshLab**  
  
File > Import Mesh > DX/SX_NOMETEMPIOmesh.obj  
Filters > Normals, Curvatures and Orientation > Transform:Translate, Center, set Origin > Posizionare il modello secondo la posizione desiderata  
considerare FOV: ca. 60 - la Y và flippata con la Z  
Filters > Mesh Layer > Matrix:Freeze Current Matrix  
Filters > Normals, Curvatures and Orientation> Matrix:Freeze Current Matrix  
File > Export Mesh As.. > NOMETEMPIODX/SXmesh.obj (sovrascrivere vecchia versione, tutte le spunte attive)  
File > Save Project As > nometempio.mlp  
  
**3. aprire una nuova sessione di Meshmixer**  
  
Import > NOMETEMPIODX/SXmesh.obj  
File > Save > nometempio.mix  
(nel caso ci sia YZ invertite - File > Import > Replace - Flip Z-Y on Import/Export)  
Edit > Close Cracks  
Analysis > Inspector (verificare e risolvere eventuali problemi Mesh) > Done  
Edit > Plane Cut (Ritagliare le parti in eccesso del modello per chiudere la parte basamentale)  
Analysis > Inspector (chiudere la Mesh) > Done  
File > Export > NOMETEMPIODX/SXmeshmixer.obj  
  
**4. aprire MeshLab**  
  
File > Open Project > nometempio.mlp  
File > Import Mesh > NOMETEMPIODX/SXmeshmixer.obj (con questo layer attivo)  
Filters > Mesh Layer > Matrix:Freeze Current Matrix  
Filters > Normals, Curvatures and Orientation> Matrix:Freeze Current Matrix  
File > Export Mesh As.. > NOMETEMPIODX/SXmeshmixer.ply (mantenere attivo solo Wedge - TextCoord + Binary Encoding + All) > OK  
  
**5. Salvare il materiale relativo a .obj e texture nella cartella Github/obj/nometempio per Michele**    
NOMETEMPIODX/SXmeshmixer.obj  
NOMETEMPIODX/SXmeshmixer.mtl  
NOMETEMPIODX/SXmeshmixer_material_0.jpg  
NOMETEMPIODX/SXmeshmixer_GeneratedMat1.jpg  
  
**6. Nexus_4.2 (dopo aver scaricato nexus e averlo un-zippato da qualche parte)**  
  
Copiare i file nella cartella un-zippata di Nexus:  
NOMETEMPIODX/SXmeshmixer.ply  
NOMETEMPIODX/SXmeshmixer.mtl  
NOMETEMPIODX/SXmeshmixer_material_0.jpg  
NOMETEMPIODX/SXmeshmixer_GeneratedMat1.jpg  
  
**6.1 Nexus_4.2 Creazione file .nxs**  
  
Aprire con Editor di Testo "Build_Nexus.bat" (tasto dx - Apri con..) e scrivere/riscrivere i comandi per la creazione del file .nxs  
  
nxsbuild NOMETEMPIODXmeshmixer.ply -o NOMETEMPIODXmeshmixer.nxs  
nxsbuild NOMETEMPIOSXmeshmixer.ply -o NOMETEMPIOSXmeshmixer.nxs  
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
    
nxscompress NOMETEMPIODXmeshmixer.nxs -o NOMETEMPIOSXmeshmixer.nxz  
nxscompress NOMETEMPIOSXmeshmixer.nxs -o NOMETEMPIOSXmeshmixer.nxz  
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
