# add-foregin-key-to-user-table-best-practise
the migration way to add foregin to user table of laravel

>I've fixed it with saving null user_id but not with 0.
>I need to make ->nullable() in migration file and when I am saving the record, I also need to save null value!
>I tried to save user_id=0 but no luck and I've fixed it with null value!
>Thanks for your help @JonasStaudenmeir!
>Hope this will helps any other user in the future if they face the same issue!

do this artisan command
>php artisan make:migration add_role_id_to_users --table=users

```php
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class AddRoleIdToUsers extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->integer('role_id')->unsigned()->after('id')->nullable();
            $table->foreign('role_id')->references('id')->on('roles');
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('users', function (Blueprint $table) {
            $table->dropForeign('users_role_id_foreign');
            $table->dropColumn('role_id');
        });
    }
}
```
