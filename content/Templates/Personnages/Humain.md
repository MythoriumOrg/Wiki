<%*
// Dossiers
const dossier_royaumes = "Lieux/Royaumes";
const dossier_comunautees = "Lieux/Comunautées";

// Fichiers
const fichiers_royaumes = app.vault.getMarkdownFiles().filter(f => f.path.startsWith(dossier_royaumes + "/"));
const fichiers_comunautees = app.vault.getMarkdownFiles().filter(f => f.path.startsWith(dossier_royaumes + "/"));

// Labels
const labels_royaumes = fichiers_royaumes.map(f => f.basename);
const labels_sexes = ["Femme", "Homme", "Inter"]
const labels_genres = ["Femme", "Homme", "Fluide", "Inter", "Non binaire", "Non défini"]
const labels_pronoms = ["Elle", "Il", "Iel"]
const labels_comunautees = fichiers_comunautees.map(f => f.basename);

// Infos
const first_name = await tp.system.prompt('Prénom du personnage');
const last_name = await tp.system.prompt('Nom du personnage');
const origine = await tp.system.suggester(labels_royaumes, labels_royaumes)
const sexe = await tp.system.suggester(labels_sexes, labels_sexes)
const genre = await tp.system.suggester(labels_genres, labels_genres)
const pronom = await tp.system.suggester(labels_pronoms, labels_pronoms)
const comunaute = await tp.system.suggester(labels_comunautees, labels_comunautees)

// génération de la note
tR = `---
first_name: ${first_name}
last_name: ${last_name}
origine: "[[${origine}]]"
sexe: ${sexe}
genre: ${genre}
pronom: ${pronom}
comunaute: "[[${comunaute}]]"
image: 
---`;

// Actions sur la note
// const titre = `${first_name} ${last_name}`;
// await tp.file.rename(titre); 
await tp.file.move(`Races/Humains/Individus/${titre}`)
%>