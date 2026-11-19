# Relatório de alterações · Maquete 3D de reforma (11/2026)

## 1. Auditoria dos arquivos recebidos
ZIP `LS_Maquete_Estudo_Preliminar_Cliente_CORRIGIDO.zip`, pasta `LS_Maquete_Interativa_Final/`:

| Arquivo | Situação |
|---|---|
| `index.html` (13,8 MB) | Última versão funcional. Motor WebGL2 próprio, sem bibliotecas externas, já com shader PBR simplificado, passeio em 1ª pessoa, plantas 2D e painel "Ideias de reforma". **Usado como base.** |
| `original_backup.html` | Maquete original. Preservada sem alterações. |
| `conceitos/*.png`, `renders/*.png` | Imagens da versão anterior. Preservadas. |

**Arquivos citados no pedido que NÃO vieram no ZIP:**
- `modelo_3d_reforma.html`: não recebido. O `original_backup.html` parece ser essa maquete original, mas não dá para confirmar só pelo nome.
- `maquete_3d_pbr.html`: não recebido. A evolução PBR já está dentro do `index.html`.
- `Planta baixa atualizada – Rua João Fernandes Cardoso Filho, 40.pdf`: não recebido. Usei como referência as plantas em imagem embutidas no HTML ("Planta atual" e "Reforma (proposta)") e `conceitos/planta_2d_referencia_atualizada.png`.

## 2. Alteração arquitetônica (Sala 1 rebaixada, −0,90 m)
- **Removidas** as duas divisórias que fechavam a Sala 1:
  - parede com arco P12 em y = 11,90 (Sala 1 / Sala 2);
  - parede com arco P13 em x = 9,26 (Sala 1 / Sala 3, jantar).
- **Mantidas** as vigas V1 e V2 sob as paredes do pavimento superior, com o fundo a 2,20 m (altura das vergas existentes no modelo). Seção e apoios devem ser confirmados por projeto estrutural.
- Mantidos os dois lances de degraus já existentes (4 espelhos de 22,5 cm). A testa do desnível ficou revestida em madeira.
- Incluído um guarda-corpo de vidro incolor nos trechos sem degrau, por segurança. Ele pode ser ocultado pelo botão da interface.
- Nenhuma outra parede, esquadria ou cobertura foi alterada. A bancada antiga da cozinha (móvel) foi substituída pelo novo mobiliário.
- **Verificação na malha 3D:** o teste conta as faces verticais entre 0,3 m e 2,0 m nas duas linhas das antigas divisórias. Na versão anterior eram 18 e 22. Nesta versão são 2 e 2, que são as faces de topo das paredes perpendiculares onde as vigas se apoiam, fora do vão. As faces das vigas, entre 2,20 m e 2,80 m, estão presentes.

## 3. Mobiliário e decoração (proporções ilustrativas)
- **Sala 1 (estar rebaixado):** sofá de 3 lugares, 2 poltronas, mesa de centro em travertino, mesa lateral, luminária de piso, pendente globo, tapete, quadro, planta e fita de LED sob as vigas.
- **Sala 2 (estar/TV):** sofá, poltrona, mesa de centro, painel ripado com rack e TV, cortina, tapete, quadro, planta e pendente.
- **Sala 3 (jantar):** mesa de 6 lugares com cadeiras estofadas, pendente linear, tapete, quadro e arandela. A parede leste ficou livre para dar acesso à escada.
- **Cozinha:** bancada em pedra com cuba sob a janela, armários inferiores e superiores, torre com refrigerador inox, **ilha com cooktop e coifa**, pendentes e objetos.
  - Folgas estimadas: cerca de 0,75 m entre a ilha e as cadeiras do jantar e cerca de 1,05 m até a bancada. Confirmar com medidas reais.
- **Ampliação:** recepção e estar (sugestão; o uso ainda será definido com a cliente) com poltronas, aparador e home office.
- **Suítes do térreo, quartos 1 e 2, estar superior e suíte superior:** camas com cabeceira estofada, criados, abajures, armários, cortinas, tapetes, quadros, estante e escrivaninhas.
- **Banheiros das suítes:** bancada com cuba, espelho, bacia e box de vidro.
- **Varanda:** 2 poltronas. Área gourmet: mantida como estava.
- **Edícula:** sem detalhamento, porque o layout interno ainda será levantado.

## 4. Renderização
- Materiais PBR por tipo: tinta, concreto, madeira, piso de madeira em réguas, porcelanato 90×90, pedra polida com veios, metal, laca, tecido (com sheen), couro, cerâmica esmaltada e vidro com Fresnel.
- Sol com sombras suaves, céu e ambiente. Um mapa zenital separa interior de exterior, para que a luz do céu não "vaze" para dentro dos ambientes.
- 68 luzes artificiais, cada uma limitada ao seu ambiente.
- Pós-processamento: SSAO (oclusão de contato), bloom das luminárias, tone mapping ACES e vinheta.
- Acumulação progressiva: quando a câmera para, a imagem é refinada até 64 quadros (antisserrilhado e sombras suaves).
- Iluminação: Dia, Fim de tarde, Nublado e Noite.

## 5. Passeio interativo
- A altura do observador segue os pisos reais da maquete: −0,90 na Sala 1, os degraus existentes e a escada até 2,95.
- Não é possível "cair" do desnível. As colisões usam as paredes extraídas da malha e o mobiliário.
- Lista para ir direto a 12 ambientes. Botão "⌂ Câmera inicial".
- **Testado em navegador headless:**
  - Sala 2 → degraus → Sala 1 (piso −0,90);
  - borda sem degrau bloqueia o avanço;
  - Sala 1 → degrau leste → jantar (piso 0);
  - escada → pavimento superior (piso 2,95);
  - teclado W, teletransporte e saída do passeio.

## 6. Limitações
- Renderização em tempo real (rasterização WebGL2), não path tracing.
- Medidas, mobiliário e materiais não são executivos.
- As vigas e o guarda-corpo precisam de validação técnica.

## 7. Ajustes de 19/11/2026
- Pavimento superior: piso trocado para o mesmo porcelanato claro (90×90) das áreas sociais do térreo, em quartos, estar, suíte e chegada da escada.
- Janela redonda da suíte superior (parede leste, x = 9,26): centralizada na parede do quarto (eixo em y = 13,80, meio do vão 11,90–15,70). Antes estava em y = 14,55.
- Armário da suíte superior transferido para a parede sul, liberando a parede da janela. Ponto do passeio "Superior · suíte" reposicionado.
- Renders 08 e 09 refeitos.
