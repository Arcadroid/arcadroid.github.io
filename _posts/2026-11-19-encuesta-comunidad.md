---
layout: single
title: "ENCUESTA: ¿Con qué juego quieren que se asocie más Dust Punk?"
date: 2026-11-19
categories:
  - Comunidad
tags:
  - Encuesta
  - Dust Punk
  - Feedback
header:
  teaser: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTDWouJ1j1LWw8k0MIy7B5bCbuPvmAyJB-Z7WXjC7fNZURzaOybU6K8CcA&s=10"
---

Queremos conocer la opinión de la comunidad mientras seguimos puliendo las mecánicas, los escenarios y la atmósfera de **Dust Punk**. 

Queremos saber qué vibra o estilo de juego te gustaría que tuviera mayor peso en la experiencia final.

A continuación puedes ver cómo van las votaciones o dejar tu propio voto para apoyar tu estilo favorito:

<div id="dustpunk-poll-container" class="dustpunk-poll">
  <div class="poll-header">
    <h3>ENCUESTA, Con que juego quieren que se asocie o parezca más Dust Punk:</h3>
    <p class="poll-subtext">Selecciona una opción para emitir tu voto.</p>
  </div>

  <div class="poll-options">
    <div class="poll-option" data-id="0" onclick="handlePollVote(0)">
      <div class="poll-bar" id="bar-0" style="width: 46%;"></div>
      <div class="poll-content">
        <span class="poll-label">Juego Estilo MadMax</span>
        <span class="poll-stats"><span id="pct-0">46%</span> (<span id="votes-0">6</span> votos)</span>
      </div>
    </div>

    <div class="poll-option" data-id="1" onclick="handlePollVote(1)">
      <div class="poll-bar" id="bar-1" style="width: 30%;"></div>
      <div class="poll-content">
        <span class="poll-label">Juego estilo Zelda desertico</span>
        <span class="poll-stats"><span id="pct-1">30%</span> (<span id="votes-1">4</span> votos)</span>
      </div>
    </div>

    <div class="poll-option" data-id="2" onclick="handlePollVote(2)">
      <div class="poll-bar" id="bar-2" style="width: 24%;"></div>
      <div class="poll-content">
        <span class="poll-label">Juego Estilo Fallout</span>
        <span class="poll-stats"><span id="pct-2">24%</span> (<span id="votes-2">3</span> votos)</span>
      </div>
    </div>
  </div>

  <div class="poll-footer">
    <span id="poll-total-text">13 personas votaron en total</span>
    <span id="poll-status" class="poll-status-msg"></span>
  </div>
</div>

<style>
  .dustpunk-poll {
    background: #19130f;
    border: 2px solid #442d1f;
    border-radius: 8px;
    padding: 24px;
    margin: 2rem 0;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.75);
    font-family: 'Rajdhani', sans-serif;
  }
  .poll-header h3 {
    margin: 0 0 8px 0;
    font-family: 'Teko', sans-serif;
    font-size: 1.85rem;
    letter-spacing: 1.5px;
    text-transform: uppercase;
    color: #f0e2d3;
    line-height: 1.2;
  }
  .poll-subtext {
    color: #a39282;
    font-size: 0.95rem;
    margin-bottom: 20px;
  }
  .poll-options {
    display: flex;
    flex-direction: column;
    gap: 14px;
  }
  .poll-option {
    position: relative;
    background: #120e0b;
    border: 2px solid #3d2516;
    border-radius: 6px;
    overflow: hidden;
    cursor: pointer;
    transition: all 0.25s ease;
    padding: 14px 18px;
  }
  .poll-option:hover {
    border-color: #c85a17;
    transform: translateX(4px);
  }
  .poll-option.voted-option {
    border-color: #e67e22;
    box-shadow: 0 0 14px rgba(230, 126, 34, 0.4);
  }
  .poll-bar {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    background: linear-gradient(90deg, rgba(200, 90, 23, 0.4), rgba(230, 126, 34, 0.65));
    transition: width 0.6s cubic-bezier(0.2, 0.8, 0.2, 1);
    z-index: 1;
    pointer-events: none;
  }
  .poll-content {
    position: relative;
    z-index: 2;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-weight: 700;
    font-size: 1.15rem;
    color: #ebdcd0;
  }
  .poll-stats {
    color: #f39c12;
    font-size: 1.05rem;
    letter-spacing: 0.5px;
  }
  .poll-footer {
    margin-top: 18px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: #9f8b7b;
    font-size: 0.95rem;
    font-weight: 600;
    border-top: 1px solid #332014;
    padding-top: 14px;
  }
  .poll-status-msg {
    color: #2ecc71;
    font-weight: bold;
    letter-spacing: 0.5px;
  }
  .poll-option.disabled {
    cursor: default;
  }
  .poll-option.disabled:hover {
    transform: none;
  }
</style>

<script>
  (function() {
    const STORAGE_KEY = 'dustpunk_poll_voted_choice_v1';
    const baseVotes = [6, 4, 3]; // 6 MadMax (46%), 4 Zelda (30%), 3 Fallout (24%) = 13 total

    function getStoredVote() {
      try {
        return localStorage.getItem(STORAGE_KEY);
      } catch(e) {
        return null;
      }
    }

    function renderPoll() {
      const userChoice = getStoredVote();
      let currentVotes = [...baseVotes];
      
      if (userChoice !== null) {
        currentVotes[parseInt(userChoice)] += 1;
      }

      const total = currentVotes.reduce((a, b) => a + b, 0);

      currentVotes.forEach((count, i) => {
        let pct = Math.round((count / total) * 100);
        // Si no ha votado el usuario, asegurar exactamente los porcentajes solicitados
        if (userChoice === null) {
          if (i === 0) pct = 46;
          if (i === 1) pct = 30;
          if (i === 2) pct = 24;
        }

        const bar = document.getElementById('bar-' + i);
        const pctEl = document.getElementById('pct-' + i);
        const votesEl = document.getElementById('votes-' + i);
        const optEl = document.querySelector('.poll-option[data-id="' + i + '"]');

        if (bar) bar.style.width = pct + '%';
        if (pctEl) pctEl.textContent = pct + '%';
        if (votesEl) votesEl.textContent = count;

        if (optEl && userChoice !== null) {
          optEl.classList.add('disabled');
          if (parseInt(userChoice) === i) {
            optEl.classList.add('voted-option');
          } else {
            optEl.classList.remove('voted-option');
          }
        }
      });

      const totalText = document.getElementById('poll-total-text');
      if (totalText) {
        totalText.textContent = total + ' personas votaron en total';
      }

      const statusEl = document.getElementById('poll-status');
      if (statusEl && userChoice !== null) {
        statusEl.textContent = '✓ ¡Voto registrado!';
      }
    }

    window.handlePollVote = function(index) {
      if (getStoredVote() !== null) return;
      try {
        localStorage.setItem(STORAGE_KEY, index);
      } catch(e) {}
      renderPoll();
    };

    if (document.readyState === 'loading') {
      document.addEventListener('DOMContentLoaded', renderPoll);
    } else {
      renderPoll();
    }
  })();
</script>
