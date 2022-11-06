# Account deletion

In the Settings section, you can delete your account under `Settings > Cancel your account`.

{% hint style="info" %}
Only an account administrator can delete the account.
{% endhint %}

**Deleting an account takes a few seconds, then everything is gone. Forever.**

## What happens if you have a subscription?

If you have a subscription, your subscription will not be cancelled automatically. We know it's a pain, but it's not because we want to f\*\*k you over. It's because we manage all the subscriptions on a different platform.

You can manage your subscriptions on [the customer portal (https://customers.monicahq.com)](https://customers.monicahq.com). By the way, you can cancel your account whenever you want on this portal.

Cancelling your subscription will not delete your account on Monica. It will simply prevent you from using your account completely with the current limit of the free plan.

## Behind the scenes

When you delete your account, here is what happens behind the scenes:

* all the contacts are immediately deleted from the database
* all the photos, documents and uploaded files are immediately deleted from the server
* all the journal entries are deleted from the database
* all the vaults are deleted from the database
* all the users are deleted and therefore, won't have access to the account anymore
* the account is deleted

To be completely transparent, all these information are deleted from the main database. However, we do have backups. Let me explain.

Every day, the database is backed up in a gigantic zip file (technically, a tgz file but it's the same concept). Everything in the database is in this zip file. Files (like documents, photos and avatars) are NOT in this backup. This backup is kept for 30 days, then it's deleted forever. The backups are stored in a separate server.

When we delete an account, your information will not be in the database anymore, but it will remain in the backup file for the next 30 days. Technically, we could restore it from this backup, but it's a real pain and it's super complex to do. We keep backups in case everything crashes and we need to do an emergency restore for every users in the server. We will never restore a single user from a backup.



