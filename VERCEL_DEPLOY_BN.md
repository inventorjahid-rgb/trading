# Vercel deployment (Bangla)

1. Upload/push the project to GitHub and import it in Vercel.
2. Build Command: `npm run build`
3. Output Directory: `dist`
4. Install Command: `npm install`
5. Set required environment variables in Vercel Project Settings → Environment Variables. Do not commit real API keys/secrets.
6. Redeploy after changing environment variables.

## Important production limitations
- The Express routes are now exposed as a Vercel serverless function under `/api/*`.
- The current database stores data in `data/db.json`. Vercel serverless filesystem writes are ephemeral and instances may not share writes. Admin changes/submissions can be lost. Migrate to a persistent database (e.g. Postgres/Supabase/Neon) before production use.
- Uploaded files are stored locally in `public/uploads`. Vercel serverless files are not persistent. Use object storage such as Vercel Blob or S3-compatible storage for uploaded images.
- Large uploads may exceed Vercel request/body limits; prefer direct-to-object-storage uploads.
- Check Vercel deployment/build logs and test `/api/public/data` after deployment. This patch prepares routing, but cannot guarantee a successful deployment without testing in your Vercel project and configuring persistent storage.
