# Tutorial Docking Menggunakan Autodock Vina versi 1.2.3 (Version 2021). 
Docking Tutorial Using Autodock Vina version (Bahasa Indonesia and English Version)
Video Tutorial dapat dilihat di link berikut:
1. Part 1: https://www.youtube.com/watch?v=Xa0SxkDritI&t=614s
2. Part 2: https://www.youtube.com/watch?v=5D89mIQpsHE   

# Perangkat lunak yang dibutuhkan 
1. Vina.exe (Version 1.2.3) download disini https://github.com/ccsb-scripps/AutoDock-Vina/releases/download/v1.2.3/vina_1.2.3_windows_x86_64.exe, vina_1.2.3_windows_x86_64.exe ubah namanya menjadi vina.exe
2. ADFR Tools (Version 1.2) https://ccsb.scripps.edu/adfr/download/1067/
3. Mgl Tools (Version 1.5.7) https://ccsb.scripps.edu/download/262/
4. Vina_Split https://github.com/purnawanpp/Docking-4ieh/blob/main/vina_split.exe
5. Windows terminal https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701
6. Avogadro (Version 1.2) https://drive.google.com/file/d/10Pw-jgnLFfNDVKT102m_w15099lUiSYI/view?usp=sharing
7. Discovery Studio (Version 2022) https://discover.3ds.com/discovery-studio-visualizer-download
8. Marvin Sketch (Version 2022) https://chemaxon.com/products/marvin/download cara install marvin sketch https://www.researchgate.net/profile/Purnawan-Pontana-Putra/publication/356913436_Tutorial_Installing_Marvin_Sketch_Software_and_Using_SWISS_ADME/links/61b2b2ee590a0b7ed6346b1a/Tutorial-Installing-Marvin-Sketch-Software-and-Using-SWISS-ADME.pdf 

# Semua file Installer docking 
1. https://drive.google.com/drive/folders/1_2wk2VlJUH8EFpytu34mPQQuF6pq4_zE?usp=sharing

# Pengaturan Path
1. Buka path, pada kolom search ketik path
2. Klik Enviromental Variabel
3. Klik Path Edit
4. Klik New, masukkan lokasi file atau folder pada path
5. Klik Ok sampai semua jendela tertutup (3 kali klik ok)
6. Yang harus dimasukaan dalam path ada 4 yaitu:      
     1. C:\Program Files (x86)\MGLTools-1.5.7, 
     2. C:\Program Files (x86)\ADFRsuite-1.0\bin and the location folder 
     3. vina. exe 
     4. vina_split.exe
# Cara mengetahui active site dan binding sitenya
1. Baca artikel proteinnya
2. Menggunakan web Uniprot https://www.uniprot.org/
3. Menggunakan aplikasi Discovery Studio, 
4. Menggunakan aplikasi server online seperti: ICM-PocketFinder, CASTp, Chimera, Qsite, Scfbio online server

# Pemisahan ligand dan protein (Menggunakan Biovia Discovery Studio)
1. Pisahkan Protein, buang air dan ligannya
2. Pisahkan ligand, buang protein, air 

# Preparasi Protein (Menggunakan Autodock Tools)
1. Dipisahkan air dan ligannya terlebih dahulu menggunakan Biovia Discovery Studio
2. Klik File Read Molecules cari protein.pdb
3. Dilakukan penambahan Hidrogen dengan Edit-Add Hidrogen-All
4. Edit tambahkan muatan gasteiger
5. Edit-Hidrogen Merge Non Polar
6. Grid-Macromolecules-Choose
7. save protein.pdbqt

# Preparasi Ligand (Menggunakan Autodock Tools)
1. Klik File Read Molecules cari ligand.pdb
2. Dilakukan penambahan Hidrogen dengan Edit-Add Hidrogen-All
3. Edit tambahkan muatan gasteiger
4. Edit-Hidrogen Merge Non Polar
5. Ligand-Input-choose
6. Pilih ligand.pdb
7. ligand-Toorsion tree-detect root
8. ligand-output-save as ligand.pdbqt

# Perintah di terminal untuk mengetahui Grid Box menggunakan Autogrid (Menggunakan Terminal)
1. python.exe prepare_gpf.py -l 4ieh_ligand.pdbqt -r 4ieh_protein.pdbqt -y
2. autogrid4 -p 4ieh_protein.gpf -l 4ieh_protein.glg

# Buat File GridBoxnya (Mengunakan Notepad) 
1. Buka file dengan 4ieh_protein.gpf
2. Catat npts 41 40 40 sebagai size x, y, z
3. Catat gridcenter -0.004 -0.187 0.078 sebagai center x, y, z
4. Buat file grid.txt didalamnya tertulis: 
center_x = -0.004
center_y = -0.187
center_z = 0.078
size_x = 40
size_y = 40
size_z = 40
5. Contoh file grid.txt dapat dilihat disini https://github.com/purnawanpp/Docking-4ieh/blob/main/grid.txt

# Prosedur Docking (Menggunakan Terminal)
1. vina --receptor 4ieh_protein.pdbqt --ligand 4ieh_ligand.pdbqt --config grid.txt --exhaustiveness=8 --out 4ieh_ligand_vina_out.pdbqt > results.txt
2. vina_split --input 4ieh_ligand_vina_out.pdbqt

# Perhitungan nilai RMSD (Menggunakan Biovia Discovery Studio)
1. Buka file 4ieh_ligand.pdbqt
2. Drag file 4ieh_ligand_vina_out_ligand_1.pdbqt
3. Klik File 4ieh_ligand.pdbqt,
4. Klik Structure-RMSD-Set Reference
5. Klik File 4ieh_ligand_vina_out_ligand_1.pdbqt
6. Klik Structure-RMSD-Heavy Atoms
7. Dibagian bawah nanti kelihatan nilai RMSDnya, nilai RMSD yang disarankan adalah <2

# Perhitungan nilai RMSD (Menggunakan Terminal Linux dan OpenBabel ver 3.1)
1. Ketik diterminal : conda activate
2. Jalankan perintah diterminal: obrms -f 4ieh_ligand.pdbqt 4ieh_ligand_vina_out.pdbqt

# Optimasi Geometri (Avogadro)
1. Buka Avogadro
2. Klik File-open-ligand/obat dengan format .mol2
3. Klik Extension-Molecular Mecahanics-Setup Force Field
4. Pilih setup Force-Field pilih UFF 
5. Klik Extension-Pilih-Optimize Geometry
6. clik Save as, save format .mol2 file

# Docking Tutorial Using Autodock Vina version 1.2.3 (2021 (English Version)
Video tutorials can be seen at the following link:
1. Part 1: https://www.youtube.com/watch?v=Xa0SxkDritI&t=614s
2. Part 2: https://www.youtube.com/watch?v=5D89mIQpsHE

# Required software
1. Vina.exe (Version 1.2.3) download here https://github.com/ccsb-scripps/AutoDock-Vina/releases/download/v1.2.3/vina_1.2.3_windows_x86_64.exe, vina_1.2.3_windows_x86_64.exe change the name to vina.exe
2. ADFR Tools (Version 1.2) https://ccsb.scripps.edu/adfr/download/1067/
3. Mgl Tools (Version 1.5.7) https://ccsb.scripps.edu/download/262/
4. Vina_Split https://github.com/purnawanpp/Docking-4ieh/blob/main/vina_split.exe
5. Windows terminal https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701
6. Avogadro (Version 1.2) https://sourceforge.net/projects/avogadro/files/latest/download
7. Discovery Studio (Version 2022) https://discover.3ds.com/discovery-studio-visualizer-download
8. Marvin Sketch (Version 2022) https://chemaxon.com/products/marvin/download how to install Marvin Sketch (Version 2022) https://chemaxon.com/products/marvin/download cara install marvin sketch https://www.researchgate.net/profile/Purnawan-Pontana-Putra/publication/356913436_Tutorial_Installing_Marvin_Sketch_Software_and_Using_SWISS_ADME/links/61b2b2ee590a0b7ed6346b1a/Tutorial-Installing-Marvin-Sketch-Software-and-Using-SWISS-ADME.pdf  

# All Software Recap
1. https://drive.google.com/drive/folders/1_2wk2VlJUH8EFpytu34mPQQuF6pq4_zE?usp=sharing

# Path Settings
1. Open the path, in the search field type path
2. Click Environmental Variables
3. Click Path Edit
4. Click New, enter the location of the file or folder in the path
5. Click Ok until all windows are closed (3 times click ok)
6. There are 4 things that must be entered in the path, namely:
     1. C:\Program Files (x86)\MGLTools-1.5.7, 
     2. C:\Program Files (x86)\ADFRsuite-1.0\bin and the location folder 
     3. vina. exe 
     4. vina_split.exe

# How to find out the active site and its binding site
1. Read the protein article
2. Using the Uniprot website https://www.uniprot.org/
3. Using the Discovery Studio application,
4. Using online server applications such as: ICM-PocketFinder, CASTp, Chimera, Qsite, Scfbio online server

# Separation of ligands and proteins (Using Biovia Discovery Studio)
1. Separate the Protein, remove the water and the ligand
2. Separate ligands, remove protein, water

# Protein Preparation (Using Autodock Tools)
1. Separate water and ligands first using Biovia Discovery Studio
2. Click File Read Molecules look for protein.pdb
3. Added Hydrogen with Edit-Add Hydrogen-All
4. Edit add gasteiger charge
5. Edit-Hydrogen Merge Non Polar
6. Grid-Macromolecules-Choose
7. save protein.pdbqt

# Ligand Preparation (Using Autodock Tools)
1. Click File Read Molecules, look for ligand.pdb
2. Added Hydrogen with Edit-Add Hydrogen-All
3. Edit add gasteiger charge
4. Edit-Hydrogen Merge Non Polar
5. Ligand-Input-choose
6. Select ligand.pdb
7. ligand-Toorsion tree-detect root
8. ligand-output-save as ligand.pdbqt

# Command in terminal to find out Grid Box using Autogrid (Using Terminal)
1. python.exe prepare_gpf.py -l 4ieh_ligand.pdbqt -r 4ieh_protein.pdbqt -y
2. autogrid4 -p 4ieh_protein.gpf -l 4ieh_protein.glg

# Create the GridBox File (Using Notepad)
1. Open the file with 4ieh_protein.gpf
2. Record npts 41 40 40 as size x, y, z
3. Record gridcenter -0.004 -0.187 0.078 as center x, y, z
4. Create a grid.txt file in it that says:
center_x = -0.004
center_y = -0.187
center_z = 0.078
size_x = 40
size_y = 40
size_z = 40
5. An example of a grid.txt file can be seen here https://github.com/purnawanpp/Docking-4ieh/blob/main/grid.txt

# Docking Procedure (Using Terminal)
1. vina --receptor 4ieh_protein.pdbqt --ligand 4ieh_ligand.pdbqt --config grid.txt --exhaustiveness=8 --out 4ieh_ligand_vina_out.pdbqt > results.txt
2. vina_split --input 4ieh_ligand_vina_out.pdbqt

# Calculation of RMSD value (Using Biovia Discovery Studio)
1. Open the file 4ieh_ligand.pdbqt
2. Drag the file 4ieh_ligand_vina_out_ligand_1.pdbqt
3. Click File 4ieh_ligand.pdbqt,
4. Click Structure-RMSD-Set Reference
5. Click File 4ieh_ligand_vina_out_ligand_1.pdbqt
6. Click Structure-RMSD-Heavy Atoms
7. At the bottom you will see the RMSD value, the recommended RMSD value is <2

# Geometry Optimization (Avogadro)
1. Open Avogadro
2. Click File-open-ligand/medicine with .mol2 . format
3. Click Extension-Molecular Mechanics-Setup Force Field
4. Select the Force-Field setup, select UFF
5. Click Extension-Select-Optimize Geometry
6. Clik Save as, save format .mol2 file
