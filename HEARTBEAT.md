# HEARTBEAT.md

## Mission Control Task Processing

When receiving a system event about Mission Control:

1. **Pull latest tasks**
   ```bash
   cd /home/ubuntu/.openclaw/workspace && git pull origin master
   ```

2. **Read tasks.json**
   - Load `/home/ubuntu/.openclaw/workspace/data/tasks.json`

3. **Find "in_progress" tasks**
   - For each task with status "in_progress":
     - Read title, description, subtasks
     - Execute the work described
     - Mark task as "review" when done
     - Add completion comment with summary

4. **Push updates**
   ```bash
   git add data/tasks.json
   git commit -m "Complete: [task title]"
   git push origin master
   ```

5. **Notify user**
   - Send message summarizing what was completed

## Auto-Pickup (Optional)

If no "in_progress" tasks found:
- Check for "backlog" tasks
- Pick highest priority
- Move to "in_progress"
- Execute and notify user

---

*This file ensures Mission Control tasks are actually processed when cron fires.*
