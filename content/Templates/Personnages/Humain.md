<%*
// Dossiers
const dossier_royaumes = "Lieux/Royaumes";

// Fichiers
const fichiers_royaumes = app.vault.getMarkdownFiles().filter(f => f.path.startsWith(dossier_royaumes + "/"));

// Options 
const options_royaumes = fichiers_royaumes.map(f => ({
	label: f.basename,
	value: f.path.replace(/\.md$/,"")
}))

// Infos
const first_name = await tp.system.prompt('Prénom du personnage');
const last_name = await tp.system.prompt('Nom du personnage');
const origine = await tp.system.suggester(options_royaumes.map(o => o.label), options_royaumes)

// génération de la note
tR = `---
first_name: ${first_name}
last_name: ${last_name}
origine: [[${origine.value}|${origine.label}]]
---`;
%>