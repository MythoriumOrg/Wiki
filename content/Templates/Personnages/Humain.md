<%*
// Dossiers
const dossier_royaumes = "Lieux/Royaumes";

// Fichiers
const fichiers_royaumes = app.vault.getMarkdownFiles().filter(f => f.path.startsWith(dossier_royaumes + "/"));

// Labels
const labels_royaumes = fichiers_royaumes.map(f => f.basename);

// Valeurs
const valeurs_royaumes = fichiers_royaumes.map(f => f.path.replace(/\.md$/,""));

// Infos
const first_name = await tp.system.prompt('Prénom du personnage');
const last_name = await tp.system.prompt('Nom du personnage');
const origine = await tp.system.suggester(labels_royaumes, valeurs_royaumes)

// génération de la note
tR = `---
first_name: ${first_name}
last_name: ${last_name}
origine: ${origine}
---`;
%>