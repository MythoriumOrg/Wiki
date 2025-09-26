<%*
// Déclaration de variables
let formatted_origine;
let formatted_comunaute;

// Functions
const slugify = s =>
  (s ?? '')
    .normalize('NFKD')
    .replace(/[\u0300-\u036f]/g, '')
    .toLocaleLowerCase('fr')
    .replace(/[^a-z0-9]+/g, '_')
    .replace(/^_+|_+$/g, '');

// Dossiers
const dossier_royaumes = "Lieux/Royaumes";
const dossier_comunautees = "Comunautées";

// Fichiers
const fichiers_royaumes = app.vault.getMarkdownFiles().filter(f => f.path.startsWith(dossier_royaumes + "/"));
const fichiers_comunautees = app.vault.getMarkdownFiles().filter(f => f.path.startsWith(dossier_comunautees + "/"));

// Labels
const labels_royaumes = fichiers_royaumes.map(f => f.basename);
const labels_sexes = ["Femme", "Homme", "Inter"]
const labels_genres = ["Femme", "Homme", "Fluide", "Inter", "Non binaire", "Non défini"]
const labels_pronoms = ["Elle", "Il", "Iel"]
const labels_comunautees = fichiers_comunautees.map(f => f.basename);

// Infos
const first_name = await tp.system.prompt('Prénom du personnage');
const last_name = await tp.system.prompt('Nom du personnage');
const sexe = await tp.system.suggester(labels_sexes, labels_sexes)
const genre = await tp.system.suggester(labels_genres, labels_genres)
const pronom = await tp.system.suggester(labels_pronoms, labels_pronoms)
const origine = await tp.system.suggester(labels_royaumes, labels_royaumes)
const comunaute = await tp.system.suggester(labels_comunautees, labels_comunautees)
const image = `[[personnage_humain_${slugify(first_name).toLowerCase()}${slugify(last_name)}.jpg]]`

// Formatteurs
if (origine){
	formatted_origine = `\norigine: "[[${origine}]]"`
} else {
	formatted_origine = ""
}

if (comunaute){
	formatted_comunaute = `\ncomunaute: "[[${comunaute}]]"`
} else {
	formatted_comunaute = ""
}

// génération de la note
tR = `---
draft: false
type: personnage
sous_type: humain
first_name: ${first_name}
last_name: ${last_name}
sexe: ${sexe}
genre: ${genre}
pronom: ${pronom}
${formatted_origine}
${formatted_comunaute}
image: "${image}"
---

## Image
!${image}`;

// Actions sur la note
const titre = `${first_name} ${last_name}`;
await tp.file.rename(titre); 
await tp.file.move(`Races/Humains/Individus/${titre}`)
%>

---

## Description physique



---

## Personnalité



---

## Rôle et vocation



---

## Habitat et mode de vie



---

## Portrait

