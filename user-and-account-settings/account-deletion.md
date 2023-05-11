# Account deletion

In the Settings section, you can delete your account under `Settings > Cancel your account`.

{% hint style="info" %}
Only an account administrator can delete the account.
{% endhint %}

**Deleting an account takes a few seconds, then everything is gone. Forever.**

## What happens if you have a subscription?

If you have a subscription with Monica and delete your account, please note that your subscription will not be cancelled automatically. This is not intended to cause inconvenience, but rather due to the fact that we manage all subscriptions on a separate platform. Therefore, if you wish to cancel your subscription, you will need to do so manually through the platform where you originally subscribed. We apologize for any inconvenience this may cause and appreciate your understanding.

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

When you delete an account in Monica, all associated information is deleted from the database. However, the data remains in the backup file for the next 30 days. While it is technically possible to restore this data from the backup, **it is a complex and difficult process that we do not undertake for individual users**. Backups are primarily kept in case of emergency server crashes, and are not intended for individual data restoration. Please ensure that you have exported and saved your data before deleting an account, as it cannot be recovered after the 30-day backup retention period has expired.
