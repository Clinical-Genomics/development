# Multithreading in perl

The threads module in perl can be used to run multiple processes in parallel. This is an example of a script that use multithreading:

	#!/usr/bin/perl
	# Template for multi threading in perl

	use strict;
	use warnings;
	use threads;

	# How many processes that will be done in parallel
	my $MAX_THREADS = 4;
	my @threads;

	# Loop that starts multiple tasks in parallel on separate threads
	for my $thread_index (1 .. $MAX_THREADS) {
		$threads[$thread_index] = threads->create({'context' => 'list'}, \&generic_sub, $thread_index);
	}

	# To return calculations from threads
	for my $thread_index (1 .. $MAX_THREADS) {
		my ($returned_tid, $returned_sum) = $threads[$thread_index]->join();
		print "Thread " . $returned_tid . " got the sum " . $returned_sum . "\n";
		say {*STDOUT} qq{The thread with thread ID $returned_tid got the sum $returned_sum};
	}

	# Subroutine that is done multiple times in parallel
	sub generic_sub {
		my ($thread_id) = @_;
		print "Thread " . $thread_id . " started\n";
		my $sum = 0;
		for my $counter (0 .. 10000000) {
			$sum = $sum + rand();
		}
		print "Thread " . $thread_id . " done\n";
		return ($thread_id, $sum);
	}

The code above can be used as a starting point when writing your own script that run processes in parallel. Most likely you want to edit the line with `my $n_threads = 4;` to allow the number of threads to be a variable.

If more processes need to be run than the number of threads that can be accessed, then the code need to be modified so the number of threds that is running is tracked. Also line with `join()` needs to ne added to the for loop where the threads are created. Since a loop constantly need to check if a new thread can be started, and if a thread is finished, it is also important to include `sleep()` in this loop.
