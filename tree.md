# Allgemeines 

Dora Projekt Beschreibung? 

> __Wichtig:__ Die Inhalte des vorliegenden Kurses wurden im __April 2026__ fertig gestellt. Alle im Text referenzierten Paragraphen, Gesetzestexte und rechtlichen Einschätzungen entsprechen dem Rechtsstand zu diesem Zeitpunkt. Da sich die Gesetzgebung und die Rechtsprechung (insbesondere im Bereich Urheberrecht und Datenschutz) ständig weiterentwickeln, sind die Nutzerinnen und Nutzer ausdrücklich dazu verpflichtet, sich anhand aktuell geltender, öffentlich zugänglicher Quellen zu versichern, dass die hier aufgeführten Regelungen weiterhin in ihrer vorliegenden Form gültig sind. Dieser Kurs dient ausschließlich als rechtliche Referenz für die Entwicklung eigener Konzepte und Ansätze im Archivwesen. Er stellt in keinem Fall eine Rechtsberatung dar und kann eine solche auch nicht ersetzen. Für verbindliche rechtliche Auskünfte im Einzelfall sollte stets eine qualifizierte Rechtsberatung hinzugezogen werden.


# Urheberrechts-Prüfung


<div id="app">
  <h2 id="question"></h2>
  <div id="answers"></div>
  <hr>
  <button onclick="goBack()">⬅ Zurück</button>
  <button onclick="restart()">🔄 Neustart</button>
</div>

<script>
// ----------------------
// Entscheidungsbaum
// ----------------------
const tree = {
  start: {
    text: "Ich möchte Daten digital zugänglich machen, die Sammlungsobjekte in meiner Institution betreffen. Bestehen Urheber- oder andere Schutzrechte an den Metadaten und Digitalisaten?",
    options: [
      { label: "Es handelt sich um Metadaten zu Objekten, die von Mitarbeitenden oder Auftragnehmer:innen erstellt wurden.", next: "q1" },
      { label: "Es handelt sich um Digitalisate von Sammlungsobjekten und/oder deren Begleitobjekte.", next: "q2" }
    ]
  },

  q1: {
    text: "Es handelt sich um Metadaten zu Objekten, die von Mitarbeitenden oder Auftragnehmer:innen erstellt wurden.",
    options: [
      { label: "Es werden ausschließlich strukturierte Information wie einzelne Wörter oder kurze Wortgruppen, Vokabularelemente, Literaturangaben, Inventarnummern, Identifier oder Werte erfasst.", next: "result0" },
      { label: "Es sind mehrzeilige Felder mit ganzen Sätzen oder Absätzen (Bildbeschreibungen, Biographien u.ä.) vorhanden.", next: "q4" }
    ]
  },

  q2: {
    text: "Bestehen urheberrechtlich relevante Schutzrechte am reproduzierten Originalwerk bzw. der Vorlage? Achtung: Es ist zu prüfen, ob andere Schutzrechte berührt werden, etwa der Datenschutz oder das Recht am eigenen Bild. Diese können ebenfalls einer Datenpublikation bzw. -weitergabe entgegenstehen.",
    options: [
      { label: "Ja, es handelt sich um ein Werk oder ein Lichtbild.", next: "q5" },
      { label: "Nein.", next: "q6" }
    ]
  },

  q4: { 
    text: "Es ist bei den Metadaten von einem Werk mit einer Schutzfrist von 70 Jahren nach dem Tod des Urhebers auszugehen.", 
    options: [
      { label: "Ja", next: "result1" },
      { label: "Nein", next: "result2" }
    ]
  },

  q5: { 
    text: "Ist die Schutzfrist des reproduzierten Originalwerks bzw. der Volage abgelaufen?", 
    options: [
      { label: "Ja", next: "result3" },
      { label: "Nein", next: "q7" },
      { label: "Weiß nicht", next: "q8"}
    ]
  },

q6: { 
    text: "Gibt es einen Vertrag über die Erstellung der Reproduktion(en) des Werkes bzw. Objektes?", 
    options: [
      { label: "Ja, darin ist die Nutzung geregelt (etwa über die Angabe einer CC-Lizenz).", next: "result4" },
      { label: "Nein, das Digitalisat wurde von technischem Personal erstellt und die Erstellung von Digitalisaten ist in der entsprechenden Tätigkeitsbeschreibung als Kernaufgabe ausgewiesen.", next: "result5" },
      { label: "Nein, die Abbildung wurde von wissenschaftlichen Mitarbeiter:innen, Volontär:innen, Ehrenamtlichen uws. erstellt.", next: "q9"}
    ]
  },


  q7: { 
    text: "Die Rechtinhaber:innen (Urheber:in(nen)/Erb:in(nen), Verwertungsgesellschaft, Verlage usw.) können recherchiert werden.", 
    options: [
      { label: "Ja", next: "q10" },
      { label: "Nein. Das Werk ist anonym oder wir haben trotz umfangreicher Recherchen keine Urheber:innen bzw. Rechteinhaber:innen ausfindig machen können.", next: "result6" },
      { label: "Nein. Wir haben nicht die Ressourcen entsprechende Recherchen zu betreiben.", next: "result7"}
    ]
  },

q8: { 
    text: "Mir sind Entstehungs- bzw. Veöffentlichungszeitpunkt des Lichtbilds bzw. Sterbejahr des Werkurhebers bekannt.", 
    options: [
      { label: "Ja", next: "q11" },
      { label: "Nein", next: "q12" }
    ]
  },


 q9: { 
    text: "Wie wurde das Digitalisat erstellt?", 
    options: [
      { label: "Es erfolgten schöpferische Eingriffe, etwa werden Beleuchtung und Objektpositionen angepasst oder Kameraparameter eingestellt, wird nachträglich eine Bildauswahl getroffen, usw.", next: "q13" },
      { label: "Es wurde werktreu (nach Protokoll) und ohne erkennbare Gestaltung (z. B. Komposition) ein Digitalisat erstellt (Schnappschüsse/Arbeitsfotos, frontale Reproduktionsfotografie eines Gemäldes oder einer Grafik, 3D-Scan einer Büste o. ä.)", next: "q14" },
      { label: "Es erfolgte eine rein technische Reproduktion, etwa mittels Filmstreifen- oder Einzugsscanner.", next: "result10"}
    ]
  },

  q10: {
      text: "Es handelt sich um ein vergriffenes Werk - es ist auf dem Markt nicht verfügbar (z.B. Einzelstück oder außer Produktion.)", 
      options: [
      { label: "Ja", next: "q15" },
      { label: "Nein", next: "result13" }
    ]
  },

  q11: {
      text: "Der Werkurheber ist länger als 70 Jahre tot bzw. die 50-Jahres-Frist (seit Veröffentlichung bzw. seit Erstellung, wenn unveröffentlicht) am Lichtbild ist abgelaufen.",
      options: [
        { label: "Ja", next: "result3" },
        { label: "Nein", next: "q16" }
      ]
  },

  q12: {
      text: "Ich kann das spätestmögliche Sterbedatum (z.B. 90 Jahre nach Werkentstehung) oder den spätestmöglichen Veröffentlichungszeitpunkt (z. B. erster mir bekannter Druck) plausibel abschätzen.",
      options: [
        { label: "Ja", next: "q11" },
        { label: "Nein", next: "result7" }
      ]
  },

  q13: {
      text: "Es ist beim Digitalisat von einem Lichtbild und damit einer Schutzfrist von 70 Jahren nach dem Tod des Urhebers auszugehen",
      options: [
        { label: "Ja", next: "result9" },
        { label: "Nein", next: "result2" }
      ]
  },

  q14: {
      text: "Handelt es sich um eine bloße Vervielfältigung eines gemeinfreien Werkes?",
      options: [
        { label: "Ja", next: "result11" },
        { label: "Nein", next: "q17" }
      ]
  },

  q15: {
      text: "Kulturinstitutionen dürfen vergriffene Werke zur Bestandsdokumentation online publizieren. Je nach Werktyp werden jährliche Zahlungen an die repräsentativen Verwertungsgesellschaften fällig.",
      options: [
        { label: "Perfekt, dann machen wir das so!", next: "result12" },
        { label: "Wir haben kein Geld für (regelmäßige) Gebühren", next: "result13" }
      ]
  },

  q16: {
      text: "Soll das Werk dauerhaft präsentiert werden, etwa in einem Webportal der Sammlung?",
      options: [
        { label: "Ja", next: "q7" },
        { label: "Nein", next: "q18" }
      ]
  },
        
  q17: {
      text: "Es ist von einem Leistungsschutzrecht am Lichtbild (§72 UrhG) mit einer Schutzfrist von 50 Jahren ohne vorherige Veröffentlichung auszugehen. Wurde innerhalb von 50 Jahren das Lichtbild publiziert, so beginnt die 50-Jahres-Frist mit der Publikation.",
      options: [
        { label: "Ja", next: "result9" },
        { label: "Nein", next: "result2" }
      ]
  },

  q18: {
      text: "Erfolgt eine Weitergabe individuell auf Anfrage direkt an Forscher:innen, Lehrende usw.?",
      options: [
        { label: "Ja", next: "result14" },
        { label: "Nein", next: "q19" }
      ]
  },

  q19: {
      text: "Sind die Daten ausschließlich vor Ort an PCs für Mitarbeiter:innen und Nutzer:innen zugänglich?",
      options: [
        { label: "Ja", next: "result15" },
        { label: "Nein", next: "q20" }
      ]
  },

  q20: {
      text: "Soll das Werk zeitlich begrenzt zur Bewerbung einer Ausstellung genutzt werden?",
      options: [
        { label: "Ja", next: "result16" },
        { label: "Nein", next: "q21" }
      ]
  },

  q21: {
      text: "Wird das Werk in einer wissenschaftlichen Publikation diskutiert oder soll in Forschung und Lehre genutzt werden?",
      options: [
        { label: "Ja", next: "result17" },
        { label: "Nein", next: "q7" }
      ]
  },
  
  
  






  result0: { text: "Eine Schöpfungshöhe wird nicht erreicht. Die Nutzung ist unproblematisch.", end: true },
  result1: { text: "Es muss eine Nutzungsvereinbarung mit den betreffenden Rechteinhaber:innen geschlossen werden. Tipp: Sofern es sich nicht um technisches Personal handelt und die Metadatenerstellung als Kernaufgabe in der Tätigkeitsbeschreibung festgehalten ist, sollten generell schriftliche Vereinbarungen über die Nachnutzung der Daten seitens der Institution geschlossen werden. Empfohlen wird für Metadaten gemeinhin die Lizenz CC0 (Public Domain) - das erlaubt etwa eine Verwendung der Daten für GND-Einträge.", end: true },
  result2: { text: "Formulierung fehlt", end: true },
  result3: { text: "Das Werk ist gemeinfrei. Eine Publikation ist unproblematisch. Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst nötig sind.", end: true },
  result4: { text: "Für Nutzungsarten, die über den Vertrag nicht abgedeckt sind, müssen gesondert Nutzungsrechte eingeholt werden.", end: true },
  result5: { text: "Eine Nutzung ist unproblematisch.", end: true },
  result6: { text: "Es handelt sich um ein verwaistes Werk. Dieses kann nach Registrierung im EUPIO-Portal unter Einhaltung einer 6-Monats-Frist veröffentlicht werden. Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst nötig sind.", end: true },
  result7: { text: "Eine Veröffentlichung sollte genau abgewogen werden, weil ein Risiko von Forderungen Dritter besteht. Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst nötig sind.", end: true },
  result8: { text: "", end: true },
  result9: { text: "Es muss eine Nutzungsvereinbarung mit den Rechteinhaber:innen geschlossen werden.", end: true },
  result10: { text: "Am Digitalisat sind keine Schutzrechte entstanden.", end: true },
  result11: { text: "An Reproduktionen gemeinfreier Werke entstehen keine neuen Schutzrechte. Eine Nutzung ist unproblematisch.", end: true },
  result12: { text: "Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst nötig sind.", end: true },
  result13: { text: "Es muss eine Nutzungsvereinbarung mit den Rechteinhaber:innen geschlossen werden. Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst nötig sind.", end: true },
  result14: { text: "Privatkopie (§ 53 UrhG). Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst vorliegen.", end: true },
  result15: { text: "Vervielfältigungsrecht (§ 60f UrhG). Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst nötig sind.", end: true },
  result16: { text: "Werbung für die Ausstellung und den öffentlichen Verkauf von Werken (§ 58 UrhG). Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst nötig sind.", end: true },
  result17: { text: "Hier greift das Zitatrecht (§ 63 UrhG) oder Schranke zur Forschungs- und Lehrfreiheit (§ 60a, 60c UrhG). Es ist zusätzlich zu klären, ob Nutzungsrechte am Digitalisat selbst nötig sind.", end: true}
  
  
         
        


};



// ----------------------
// State
// ----------------------
let history = [];
let current = "start";

// ----------------------
// Render-Funktion
// ----------------------
function render(nodeKey) {
  const node = tree[nodeKey];
  const q = document.getElementById("question");
  const a = document.getElementById("answers");

  q.innerText = node.text;
  a.innerHTML = "";

  if (node.end) return;

  node.options.forEach(opt => {
    const btn = document.createElement("button");
    btn.innerText = opt.label;
    btn.style.display = "block";
    btn.style.margin = "10px 0";
    btn.onclick = () => {
      history.push(current);
      current = opt.next;
      render(current);
    };
    a.appendChild(btn);
  });
}

// ----------------------
// Navigation
// ----------------------
window.goBack = function() {
  if (history.length > 0) {
    current = history.pop();
    render(current);
  }
}

window.restart = function() {
  history = [];
  current = "start";
  render(current);
};

// ----------------------
// Init
// ----------------------
render(current);
</script>

<style>
#app {
  max-width: 700px;
  margin: auto;
  font-family: sans-serif;
}

button {
  padding: 10px;
  width: 100%;
  cursor: pointer;
}
</style>

---
