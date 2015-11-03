title: mac osx10.11下pip安装gevent失败
date: 2015-11-03 15:19:08
tags:
- mac osx EI Capitan
- pip
- gevent
---
安装环境：

- mac osx EI Capitan
- python 2.7.6

pip安装gevent过程中, 出现以下错误(错误代码类似):
<!-- more -->
<pre><code>    clang -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes -I /opt/local/include -L /opt/local/lib -U__llvm__ -DLIBEV_EMBED=1 -DEV_COMMON= -DEV_CLEANUP_ENABLE=0 -DEV_EMBED_ENABLE=0 -DEV_PERIODIC_ENABLE=0 -Ibuild/temp.macosx-10.11-x86_64-2.7/libev -Ilibev -I/usr/local/include -I/usr/local/opt/openssl/include -I/usr/local/opt/sqlite/include -I/usr/local/Cellar/python/2.7.10_2/Frameworks/Python.framework/Versions/2.7/include/python2.7 -c gevent/gevent.core.c -o build/temp.macosx-10.11-x86_64-2.7/gevent/gevent.core.o
  clang: warning: argument unused during compilation: '-L/opt/local/lib'
  In file included from gevent/gevent.core.c:249:
  In file included from gevent/libev.h:2:
  libev/ev.c:483:48: warning: '/*' within block comment [-Wcomment]
  /*#define MIN_INTERVAL  0.00000095367431640625 /* 1/2**20, good till 2200 */
                                                 ^
  libev/ev.c:1029:42: error: '_Noreturn' keyword must precede function declarator
    ecb_inline void ecb_unreachable (void) ecb_noreturn;
                                           ^~~~~~~~~~~~
    _Noreturn
  libev/ev.c:832:26: note: expanded from macro 'ecb_noreturn'
    #define ecb_noreturn   _Noreturn
                           ^
  libev/ev.c:1625:31: warning: 'extern' variable has an initializer [-Wextern-initializer]
    EV_API_DECL struct ev_loop *ev_default_loop_ptr = 0; /* needs to be initialised to make it a definition despite extern */
                                ^
  libev/ev.c:1796:7: warning: unused variable 'ocur_' [-Wunused-variable]
        array_needsize (ANPENDING, pendings [pri], pendingmax [pri], w_-&gt;pending, EMPTY2);
        ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  libev/ev.c:1807:3: warning: unused variable 'ocur_' [-Wunused-variable]
    array_needsize (W, rfeeds, rfeedmax, rfeedcnt + 1, EMPTY2);
    ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  libev/ev.c:1934:7: warning: unused variable 'ocur_' [-Wunused-variable]
        array_needsize (int, fdchanges, fdchangemax, fdchangecnt, EMPTY2);
        ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  In file included from gevent/gevent.core.c:249:
  In file included from gevent/libev.h:2:
  In file included from libev/ev.c:2484:
  libev/ev_kqueue.c:50:3: warning: unused variable 'ocur_' [-Wunused-variable]
    array_needsize (struct kevent, kqueue_changes, kqueue_changemax, kqueue_changecnt, EMPTY2);
    ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  In file included from gevent/gevent.core.c:249:
  In file included from gevent/libev.h:2:
  In file included from libev/ev.c:2490:
  libev/ev_poll.c:66:7: warning: unused variable 'ocur_' [-Wunused-variable]
        array_needsize (struct pollfd, polls, pollmax, pollcnt, EMPTY2);
        ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  libev/ev.c:3648:34: warning: '&amp;' within '|' [-Wbitwise-op-parentheses]
    fd_change (EV_A_ fd, w-&gt;events &amp; EV__IOFDSET | EV_ANFD_REIFY);
                         ~~~~~~~~~~^~~~~~~~~~~~~ ~
  libev/ev.c:3648:34: note: place parentheses around the '&amp;' expression to silence this warning
    fd_change (EV_A_ fd, w-&gt;events &amp; EV__IOFDSET | EV_ANFD_REIFY);
                                   ^
                         (                      )
  libev/ev.c:3687:3: warning: unused variable 'ocur_' [-Wunused-variable]
    array_needsize (ANHE, timers, timermax, ev_active (w) + 1, EMPTY2);
    ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  libev/ev.c:4367:5: warning: unused variable 'ocur_' [-Wunused-variable]
      array_needsize (ev_idle *, idles [ABSPRI (w)], idlemax [ABSPRI (w)], active, EMPTY2);
      ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  libev/ev.c:4407:3: warning: unused variable 'ocur_' [-Wunused-variable]
    array_needsize (ev_prepare *, prepares, preparemax, preparecnt, EMPTY2);
    ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  libev/ev.c:4445:3: warning: unused variable 'ocur_' [-Wunused-variable]
    array_needsize (ev_check *, checks, checkmax, checkcnt, EMPTY2);
    ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  libev/ev.c:4592:3: warning: unused variable 'ocur_' [-Wunused-variable]
    array_needsize (ev_fork *, forks, forkmax, forkcnt, EMPTY2);
    ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  libev/ev.c:4675:3: warning: unused variable 'ocur_' [-Wunused-variable]
    array_needsize (ev_async *, asyncs, asyncmax, asynccnt, EMPTY2);
    ^
  libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
        int ecb_unused ocur_ = (cur);                                     \
                       ^
  14 warnings and 1 error generated.
  error: command 'clang' failed with exit status 1

  ----------------------------------------
  Failed building wheel for gevent
Failed to build gevent
Installing collected packages: gevent
  Running setup.py install for gevent
    Complete output from command /usr/local/opt/python/bin/python2.7 -c "import setuptools, tokenize;__file__='/private/var/folders/q8/1c24n_wj6kzc6kgl7629pwyh0000gn/T/pip-build-3zCPVx/gevent/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /var/folders/q8/1c24n_wj6kzc6kgl7629pwyh0000gn/T/pip-9VpZCX-record/install-record.txt --single-version-externally-managed --compile:
    running install
    running build
    running build_py
    running build_ext
    building 'gevent.core' extension
    clang -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes -I /opt/local/include -L /opt/local/lib -U__llvm__ -DLIBEV_EMBED=1 -DEV_COMMON= -DEV_CLEANUP_ENABLE=0 -DEV_EMBED_ENABLE=0 -DEV_PERIODIC_ENABLE=0 -Ibuild/temp.macosx-10.11-x86_64-2.7/libev -Ilibev -I/usr/local/include -I/usr/local/opt/openssl/include -I/usr/local/opt/sqlite/include -I/usr/local/Cellar/python/2.7.10_2/Frameworks/Python.framework/Versions/2.7/include/python2.7 -c gevent/gevent.core.c -o build/temp.macosx-10.11-x86_64-2.7/gevent/gevent.core.o
    clang: warning: argument unused during compilation: '-L/opt/local/lib'
    In file included from gevent/gevent.core.c:249:
    In file included from gevent/libev.h:2:
    libev/ev.c:483:48: warning: '/*' within block comment [-Wcomment]
    /*#define MIN_INTERVAL  0.00000095367431640625 /* 1/2**20, good till 2200 */
                                                   ^
    libev/ev.c:1029:42: error: '_Noreturn' keyword must precede function declarator
      ecb_inline void ecb_unreachable (void) ecb_noreturn;
                                             ^~~~~~~~~~~~
      _Noreturn
    libev/ev.c:832:26: note: expanded from macro 'ecb_noreturn'
      #define ecb_noreturn   _Noreturn
                             ^
    libev/ev.c:1625:31: warning: 'extern' variable has an initializer [-Wextern-initializer]
      EV_API_DECL struct ev_loop *ev_default_loop_ptr = 0; /* needs to be initialised to make it a definition despite extern */
                                  ^
    libev/ev.c:1796:7: warning: unused variable 'ocur_' [-Wunused-variable]
          array_needsize (ANPENDING, pendings [pri], pendingmax [pri], w_-&gt;pending, EMPTY2);
          ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    libev/ev.c:1807:3: warning: unused variable 'ocur_' [-Wunused-variable]
      array_needsize (W, rfeeds, rfeedmax, rfeedcnt + 1, EMPTY2);
      ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    libev/ev.c:1934:7: warning: unused variable 'ocur_' [-Wunused-variable]
          array_needsize (int, fdchanges, fdchangemax, fdchangecnt, EMPTY2);
          ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    In file included from gevent/gevent.core.c:249:
    In file included from gevent/libev.h:2:
    In file included from libev/ev.c:2484:
    libev/ev_kqueue.c:50:3: warning: unused variable 'ocur_' [-Wunused-variable]
      array_needsize (struct kevent, kqueue_changes, kqueue_changemax, kqueue_changecnt, EMPTY2);
      ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    In file included from gevent/gevent.core.c:249:
    In file included from gevent/libev.h:2:
    In file included from libev/ev.c:2490:
    libev/ev_poll.c:66:7: warning: unused variable 'ocur_' [-Wunused-variable]
          array_needsize (struct pollfd, polls, pollmax, pollcnt, EMPTY2);
          ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    libev/ev.c:3648:34: warning: '&amp;' within '|' [-Wbitwise-op-parentheses]
      fd_change (EV_A_ fd, w-&gt;events &amp; EV__IOFDSET | EV_ANFD_REIFY);
                           ~~~~~~~~~~^~~~~~~~~~~~~ ~
    libev/ev.c:3648:34: note: place parentheses around the '&amp;' expression to silence this warning
      fd_change (EV_A_ fd, w-&gt;events &amp; EV__IOFDSET | EV_ANFD_REIFY);
                                     ^
                           (                      )
    libev/ev.c:3687:3: warning: unused variable 'ocur_' [-Wunused-variable]
      array_needsize (ANHE, timers, timermax, ev_active (w) + 1, EMPTY2);
      ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    libev/ev.c:4367:5: warning: unused variable 'ocur_' [-Wunused-variable]
        array_needsize (ev_idle *, idles [ABSPRI (w)], idlemax [ABSPRI (w)], active, EMPTY2);
        ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    libev/ev.c:4407:3: warning: unused variable 'ocur_' [-Wunused-variable]
      array_needsize (ev_prepare *, prepares, preparemax, preparecnt, EMPTY2);
      ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    libev/ev.c:4445:3: warning: unused variable 'ocur_' [-Wunused-variable]
      array_needsize (ev_check *, checks, checkmax, checkcnt, EMPTY2);
      ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    libev/ev.c:4592:3: warning: unused variable 'ocur_' [-Wunused-variable]
      array_needsize (ev_fork *, forks, forkmax, forkcnt, EMPTY2);
      ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    libev/ev.c:4675:3: warning: unused variable 'ocur_' [-Wunused-variable]
      array_needsize (ev_async *, asyncs, asyncmax, asynccnt, EMPTY2);
      ^
    libev/ev.c:1758:22: note: expanded from macro 'array_needsize'
          int ecb_unused ocur_ = (cur);                                     \
                         ^
    14 warnings and 1 error generated.
    error: command 'clang' failed with exit status 1

    ----------------------------------------
Command "/usr/local/opt/python/bin/python2.7 -c "import setuptools, tokenize;__file__='/private/var/folders/q8/1c24n_wj6kzc6kgl7629pwyh0000gn/T/pip-build-3zCPVx/gevent/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /var/folders/q8/1c24n_wj6kzc6kgl7629pwyh0000gn/T/pip-9VpZCX-record/install-record.txt --single-version-externally-managed --compile" failed with error code 1 in /private/var/folders/q8/1c24n_wj6kzc6kgl7629pwyh0000gn/T/pip-build-3zCPVx/gevent
</code></pre>

系统升级前，这样安装是没问题的, 升级后就悲剧了.
通过强大的stackoverflow，几番查询后，问题终于解决了，记录一下做备用。

解决方案如下:

	CFLAGS='-std=c99' pip install gevent

主要原因是, osx10.11系统中, clang默认采用c11取代了之前的c99; 在这里, 我们临时退回c99即可.
