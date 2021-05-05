
fs = openFile @"C:\Program Files (x86)\Steam\steamapps\common\Battlefield 2\mods\vanilla\Objects\staticobjects\conFiles.txt"

while not eof fs do(

	myMesh = readline fs
	conPath = substituteString myMesh ".con" ""
	meshName = filterString myMesh "\\"
	meshFolder = DeleteItem meshName meshName.count
	meshFolderString = ""
	for i = 1 to meshFolder.count do(
		meshFolderString = meshFolderString + meshFolder[i] + "\\" 
	)
	meshName = filterString myMesh "\\"
	finalMeshFile = substituteString meshName[meshName.count] ".con" ""
	collisionMesh = meshFolderString + "meshes\\" + finalMeshFile + ".collisionmesh"
	
	collisionMesh = substituteString collisionMesh "\"" ""
	print collisionMesh


    if doesFileExist collisionMesh do (
			colFilePath = @"C:\Program Files (x86)\Steam\steamapps\common\Battlefield 2\mods\vanilla\Objects\staticobjects\colTemp10.txt"
			colFile = (createfile colFilePath)
			format "%" collisionMesh to:colFile
			close colFile
		
			colfs = openFile colFilePath
			while not eof colfs do(
				colfileline = readline colfs
				ImportColMesh colfileline
				
				
				select $nonvis_...*
				max select invert
				max delete
				
				

			)
			close colfs
			
	) 
	BF2ObjectImport fname:myMesh forLm:false useAlternate:false si:false

try(
	local counter = 1

file = conPath + "_textures.txt"
matfile = (createfile file)
materialOutput = ""
		
	for mat in scenematerials do
	(
		myCounter = counter as string
		mat.name = myCounter + "||" + mat.name
		
		materialFile = BF2MatInfo.getSingle mat
		matTextures = materialFile.textures as string
		matTextures = substituteString matTextures "#(" "["
		matTextures = substituteString matTextures ")" "]"
		materialOutput = materialOutput + materialFile.materialName + "\n"
		materialOutput = materialOutput + "{" + "\n"
		materialOutput = materialOutput + matTextures + "\n"
		materialOutput = materialOutput + "}" + "\n"
		
		
		
		counter = counter + 1
	)
print materialOutput to:matfile	


	
) catch ( 
	print "No folder found"
)

-- Reparent collision if exists
if $nonvis_ != undefined then (
	$nonvis_.parent = $geom0
)

	

select $* -- Select All
exportfile conPath #noprompt selectedOnly:true using:FBXEXP
resetMaxFile #noprompt
  
)
close fs
