
whenever you get a problem, you check the error.log, you will have the problem solved
by using
`cat /var/log/mysql/error.log | grep ERROR`
or
`tail -30 /var/log/mysql/error.log`

if you are in the mysql shell, user `show warnings`, to see the warnings.

change your password:
	https://www.percona.com/blog/2016/03/16/change-user-password-in-mysql-5-7-with-plugin-auth_socket/
