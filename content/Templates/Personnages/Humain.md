---
type: "personnage"
sousType: "Humain"
nom: "<% await tp.system.prompt('Nom') %>"
prenom: "<% await tp.system.prompt('prénom') %>"
genre: "<%* tR = await tp.system.suggester(['Masculin','Féminin','Autre','Inconnu'], ['M','F','X','?']); tR %>"
sexe: "<%* tR = await tp.system.suggester(['Masculin','Féminin','Autre'], ['M','F','X']); tR %>"
dateNaissance: "<% await tp.system.prompt('Date de naissance (YYYY-MM-DD ou « Inconnue »)') %>"
origine: "<%*
const folder = "Lieux/Royaumes";
const files = app.vault.getMarkdownFiles()
  .filter(f => f.path.startsWith(folder + "/")); // inclut les sous-dossiers

if (files.length === 0) {
  tR = '"Inconnu"'; // fallback texte
} else {
  // étiquettes lisibles (basename) + valeurs (chemin sans .md) pour éviter les doublons
  const labels = files.map(f => f.basename);
  const values = files.map(f => f.path.replace(/\.md$/, ""));
  const picked = await tp.system.suggester(labels, values);
  tR = picked ? `[[${picked}]]` : '"N/A"';
}
%>"
---