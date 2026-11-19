# Sunken Market story upgrade

## Included in this build
- Explorer profile with display name and emblem.
- Local-device save data for profile, settings, completed chapter and unlock count.
- Six-chapter story map with chapter summaries and objectives.
- Chapter 1 story intro before the existing underwater treasure-recovery gameplay.
- Chapter completion records and next-chapter story unlock flow.
- Settings for sound, look sensitivity and a battery-saver render scale.
- Existing Three.js world, controls, treasure collection and mobile controls retained.

## Important scope note
This is a front-end prototype. Profiles and progress are stored in the browser's localStorage; there is no secure online account, password authentication, cloud sync, multiplayer, or server database. Chapter 1 uses the existing playable treasure-recovery world. Chapters 2–6 currently have their narrative, map entries and unlock structure, but their distinct environments, quests, puzzles and cutscenes still need to be built.

## Deploy
Replace the existing `index.html` in your GitHub repository with this one. Keep your existing `models/` folder and other project files. Vercel should redeploy automatically if connected to that repository.
