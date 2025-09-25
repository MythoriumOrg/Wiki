<%*
// Dossiers
const dossier_royaumes = "Lieux/Royaumes";

// Fichiers
const fichiers_royaumes = app.vault.getMarkdownFiles().filter(f => f.path.startsWith(dossier_royaumes + "/"));

// Labels
const labels_royaumes = fichiers_royaumes.map(f => f.basename);
const labels_genres = ["Femme", "Homme", "Fluide", "Inter", "Non binaire", "Non défini"]
const labels_sexes = ["Femme", "Homme", "Inter"]
const labels_pronoms = ["Elle", "Il", "Iel"]

// Infos
const first_name = await tp.system.prompt('Prénom du personnage');
const last_name = await tp.system.prompt('Nom du personnage');
const origine = await tp.system.suggester(labels_royaumes, labels_royaumes)
const genre = await tp.system.suggester()

// génération de la note
tR = `---
first_name: ${first_name}
last_name: ${last_name}
origine: "[[${origine}]]"
---`;
%>