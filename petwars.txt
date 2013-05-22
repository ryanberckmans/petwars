/var _ {1    2     3     4      5   6    7  8  9  10  11  12  13  14  15 16  17     18   19     20    21             22   23	    24  25  26  27} {}
/var _ {name level class weapon hp  mana ac hr dr str wis int dex con xp pts prompt wins losses queue person against sanc striking  war thi cle mag} {}
/showme {@AnsiBold()@ForeRed()Type @ForeCyan()help @ForeRed()for a list of commands}

/setfloatprec 2
/action {# Chat connection with %5 lost.} {/itemdelete {petwars2} {$5}} {Petwars}
/action {%0 chats to you, 'acce} {checkaccept @CapName(@LTrim($0))} {Petwars}
/action {%0 chats to you, 'cast %1'} {/if {@InList(petwars1,@CapName(@LTrim($0)))==1} {/if {@InList(spells,$1)==1} {/if {@GetArray(petwars,@Var(x@CapName(@LTrim($0))),16)>=@Var(spell$1)} {/assign {petwars} {@Var(x@CapName(@LTrim($0))),@Var(spell$1arr)} {1};/assign {petwars} {@Var(x@CapName(@LTrim($0))),16} {@Math(@GetArray(petwars,@Var(x@CapName(@LTrim($0))),16)-@Var(spell$1))};/emote @LTrim(@LTrim($0)) Your pet will have $1 during the next fight} {/emote @LTrim($0) You do not have enough points for that spell}} {/emote @LTrim($0) That is not a valid spell}} {/emote @LTrim($0) @AnsiBold()@ForeRed()You need to @ForeCyan()create @ForeRed()a pet first}} {Petwars}
/action {%0 chats to you, 'challenge %1'} {/if {@Exists(x@CapName($1))==1} {checkchallenge @CapName(@LTrim($0)) @CapName(@RTrim(@LTrim($1)))} {/emote @LTrim($0) @AnsiBold()@ForeCyan()@CapName($1) @ForeRed()does not have a pet!}} {Petwars}
/action {%0 chats to you, 'costs} {/emote @LTrim($0) @AnsiBold()@ForeRed()Costs:@Chr(10)@AnsiBold()@ForeCyan()Upgrade    Cost  Max@Chr(10)@AnsiBold()@ForeBlue()@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(10)@ForeCyan()hp          6    10000@Chr(10)mana        4    5000@Chr(10)hr          4    100@Chr(10)dr          6    100@Chr(10)ac          3    -100@Chr(10)str         6    18@Chr(10)wis         6    18@Chr(10)int         6    18@Chr(10)dex         6    18@Chr(10)con         6    18@Chr(10)weapon      60   platinum (7)@Chr(10)sanc        8@Chr(10)striking    6} {Petwars}
/action {%0 chats to you, 'creat} {checkinlist @CapName(@LTrim($0))} {Petwars}
/action {%1 chats to you, 'decli} {/var {x} {@LTrim(@CapName($1))};/if {@GetArray(petwars,@Var(x$x),20)==2} {decline $x} {declinecancel You have not been challenged}} {Petwars}
/action {%1 chats to you, 'cance} {/var {x} {@LTrim(@CapName($1))};/if {@GetArray(petwars,@Var(x$x),20)==1} {cancel $x} {declinecancel You have not initiated a challenge}} {Petwars}

/alias {declinecancel %2} {/if {@GetArray(petwars,@Var(x@CapName(@LTrim($0))),20)==3 || @GetArray(petwars,@Var(x@CapName(@LTrim($0))),20)==2} {/emote @LTrim($0) @AnsiBold()$2} {}} {Petwars}
/alias {cancel %2} {/assign {petwars} {@Var(x$x),20} {0};/emote $x @AnsiBold()@ForeRed()You have canceled you challenge to @ForeCyan()@GetArray(petwars,@Var(x$x),21);/assign {petwars} {@Var(x@GetArray(petwars,@Var(x$x),21)),20} {0};/emote @GetArray(petwars,@Var(x$x),21) @AnsiBold()@ForeCyan()@LTrim(@CapName($2)) @ForeRed()has canceled his or her challenge} {Petwars}
/alias {decline %2} {/assign {petwars} {@Var(x$x),20} {0};/emote $x @AnsiBold()@ForeRed()You have declined @ForeCyan()@GetArray(petwars,@Var(x$x),21)@ForeRed()'s challenge;/assign {petwars} {@Var(x@GetArray(petwars,@Var(x$x),21)),20} {0};/emote @GetArray(petwars,@Var(x$x),21) @AnsiBold()@ForeCyan()@LTrim(@CapName($2)) @AnsiBold()@ForeRed()has declined your challenge} {Petwars}

/action {%0 chats to you, 'help} {/chat @LTrim($0) @AnsiBold()@ForeRed()Commands:@Chr(10)@ForeCyan()create pet @ForeRed()- creates your pet@Chr(10)@ForeCyan()name <name> @ForeRed()- names your pet@Chr(10)@ForeCyan()stats @ForeRed()- check your pet's stats@Chr(10)@ForeCyan()challenge <player> @ForeRed()- challenge someone to battle@Chr(10)@ForeCyan()accept @ForeRed()- accept a battle@Chr(10)@ForeCyan()cancel @ForeRed()- cancel a challenge before being entered into the queue@Chr(10)@ForeCyan()decline@ForeRed() - decline from a battle@Chr(10)@ForeCyan()costs @ForeRed()- shows the cost and max of each upgrade@Chr(10)@ForeCyan()increase <stat> <x> @ForeRed()- increases stat x numbers of times, at a cost@Chr(10)@ForeCyan()increase <stat> max @ForeRed()- increases stat as many times as possible@Chr(10)@ForeCyan()cast <spell> @ForeRed()- will bestow spell upon your pet for next battle@Chr(10)@ForeCyan()reset pet - @ForeRed()makes a new, level 1 noclass pet for you (WARNING)@Chr(10)@ForeCyan()glance <player> @ForeRed()- glances at player's pet@Chr(10)@ForeCyan()who @ForeRed()- shows who is on Petwars@Chr(10)@ForeCyan()queue @ForeRed()- displays who is in the queue@Chr(10)@ForeCyan()look board @ForeRed()- looks at messages on board@Chr(10)@ForeCyan()leavemessage <message> @ForeRed()- leaves a message for people to read@Chr(10)@ForeCyan()message <#> @ForeRed()- reads post #@Chr(10)@ForeCyan()reclass <class> @ForeRed()- changes your pet to different class (level 21)@Chr(10)@ForeCyan()toggleprompt @ForeRed()- toggles prompt on or off} {Petwars}
/action {%0 chats to you, 'increase %7'} {/if {@StrStr($7,max)==-1 && @StrStr($7,ac)==-1} {/if {@InList(petwars1,@CapName(@LTrim($0)))==1} {/if {@InList(stco,@Word($7,1))==1} {checkincrease $7} {/emote @LTrim($0) That stat is not available to upgrade}} {/emote @LTrim($0) @AnsiBold()@ForeRed()You need to @ForeCyan()create @ForeRed()a pet first}} {}} {Petwars}
/action {%0 chats to you, 'increase %8 max'} {/if {@StrStr($8,ac)==-1} {/if {@InList(petwars1,@CapName(@LTrim($0)))==1} {/if {@InList(stco,$8)==1} {checkincrease $8 @Math(@GetArray(petwars,@Var(x@CapName(@LTrim($0))),16)/@Var(stco$8))} {/emote @LTrim($0) That stat is not available to upgrade}} {/emote @LTrim($0) @AnsiBold()@ForeRed()You need to @ForeCyan()create @ForeRed()a pet first}} {}} {Petwars}
/action {%0 chats to you, 'increase ac %9'} {/if {@StrStr($9,max)==-1} {/if {@InList(petwars1,@CapName(@LTrim($0)))==1} {checkacincrease $9} {/emote @LTrim($0) @AnsiBold()@ForeRed()You need to @ForeCyan()create @ForeRed()a pet first}} {}} {Petwars}
/action {%0 chats to you, 'increase ac max'} {/if {@InList(petwars1,@CapName(@LTrim($0)))==1} {checkacincrease @Math(@GetArray(petwars,@Var(x@CapName(@LTrim($0))),16)/@Var(stcoac))} {/emote @LTrim($0) @AnsiBold()@ForeRed()You need to @ForeCyan()create @ForeRed()a pet first}} {Petwars}


/action {%0 chats to you, 'reset pet} {/if {@InList(petwars1,@CapName(@LTrim($0)))==1} {/emote @LTrim($0) You have a new pet!;/assign {petwars} {@Var(x@CapName(@LTrim($0))),1} {NoName};/assign {petwars} {@Var(x@CapName(@LTrim($0))),2} {1};/assign {petwars} {@Var(x@CapName(@LTrim($0))),3} {0};/assign {petwars} {@Var(x$0),24} {0};/assign {petwars} {@Var(x$0),25} {0};/assign {petwars} {@Var(x@CapName(@LTrim($0))),4} {1};/assign {petwars} {@Var(x@CapName(@LTrim($0))),5} {100};/assign {petwars} {@Var(x@CapName(@LTrim($0))),6} {50};/assign {petwars} {@Var(x@CapName(@LTrim($0))),7} {100};/assign {petwars} {@Var(x@CapName(@LTrim($0))),8} {20};/assign {petwars} {@Var(x@CapName(@LTrim($0))),9} {10};/assign {petwars} {@Var(x@CapName(@LTrim($0))),10} {10};/assign {petwars} {@Var(x@CapName(@LTrim($0))),11} {10};/assign {petwars} {@Var(x@CapName(@LTrim($0))),12} {10};/assign {petwars} {@Var(x@CapName(@LTrim($0))),13} {10};/assign {petwars} {@Var(x@CapName(@LTrim($0))),14} {10};/assign {petwars} {@Var(x@CapName(@LTrim($0))),15} {0};/assign {petwars} {@Var(x@CapName(@LTrim($0))),16} {5};/assign {petwars} {@Var(x@CapName(@LTrim($0))),17} {no};/assign {petwars} {@Var(x@CapName(@LTrim($0))),18} {0};/assign {petwars} {@Var(x@CapName(@LTrim($0))),19} {0};/assign {petwars} {@Var(x@CapName(@LTrim($0))),20} {0};/assign {petwars} {@Var(x@CapName(@LTrim($0))),21} {none};/emote @LTrim($0) Use stats to see your pet's stats.} {}} {}
/action {%0 is on right now!} {/itemadd {player} {$0}} {}
/action {%2 chats to you, 'who} {getwhoison;/emote @LTrim($2) @Chr(10)@Var(whoison)} {Petwars}
/action {%4 chats to you, 'glance %9'} {/if {@Var(petbattle@Var(petbattle))} {/if {"@Var(pet1)"=="@CapName($9)"} {/emote @LTrim($4) @AnsiBold()@ForeYellow()@Var(pet1)'s pet, @ForeCyan()@GetArray(petwars,@Var(x@CapName(@Var(pet1))),1)@ForeYellow() @Var(pet1cond)} {/emote @LTrim($4) @AnsiBold()@ForeYellow()@Var(pet2)'s pet, @ForeCyan()@GetArray(petwars,@Var(x@CapName(@Var(pet2))),1)@ForeYellow() @Var(pet2cond)}} {/emote @LTrim($4) There is not a battle underway.}} {Petwars}
/action {%5 chats to you, 'leavemessage %2'} {/if {@Len($2)<100} {/itemadd {messages} {@AnsiBold()@ForeCyan()@LTrim($5)@ForeBlue(): @ForeGreen()$2}} {}} {Petwars}
/action {%6 chats to you, 'look board} {/if {@GetCount(messages)>0} {getmessages;/emote @LTrim($6) @Chr(10)@Var(messages)} {/emote @LTrim($6) The message board is empty} {Petwars}} {}
/action {%6 chats to you, 'name %8'} {/if {@InList(petwars1,@CapName(@LTrim($6)))==1} {/if {@WordCount($8)==1} {setname @CapName(@LTrim($6)) $8} {/emote @LTrim($6) To set your name use name <name>}} {/emote @LTrim($6) Make a pet first, or use a name with less letters}} {Petwars}
/action {%6 chats to you, 'queue} {/if {@GetCount(queue)>0} {getqueue;/emote @LTrim($6) @Chr(10)@Var(queue)} {/emote @LTrim($6) The queue is empty}} {Petwars}
/action {%7 chats to you, 'message %2'} {/if {@GetCount(messages)>0} {/if {$2<=@GetCount(messages)} {/emote @LTrim($7) @GetItem(messages,$2)} {/emote @LTrim($7) Invalid message}} {/emote @Ltrim($7) The message board is empty}} {Petwars}
/action {%8 chats to you, 'reclass %4'} {/if {@GetArray(petwars,@Var(x@CapName(@LTrim($8))),2)==21 && @InList(class,$4)==1} {doreclass @CapName(@LTrim($8)) $4} {/emote @LTrim($8) Your pet is not level 21}} {Petwars}
/action {%8 chats to you, 'stats %7'} {/if {@InList(petwars1,@CapName($7))==1} {/emote @LTrim($8) @AnsiBold()@ForeWhite()@CapName($7)@ForeBlue()[@ForeGreen()L@ForeCyan()@GetArray(petwars,@Var(x@CapName($7)),2)@ForeBlue()|@ForeMagenta()@GetArray(petwars,@Var(x@CapName($7)),3)@ForeBlue()|@ForeYellow()@Var(weap@GetArray(petwars,@Var(x@CapName($7)),4))@ForeBlue()|@ForeRed()@GetArray(petwars,@Var(x@CapName($7)),18)@ForeBlue()/@ForeRed()@GetArray(petwars,@Var(x@CapName($7)),19)@ForeBlue()]} {/emote @LTrim($8) @AnsiBold()@ForeCyan()@CapName($7) @ForeRed()does not have a pet}} {Petwars}
/action {%8 chats to you, 'stats'} {/if {@InList(petwars1,@CapName(@LTrim($8)))==1} {givestats @LTrim($8)} {/emote @LTrim($8) @AnsiBold()@ForeRed()You need to @ForeCyan()create@ForeRed() a pet first}} {Petwars}
/action {%9 chats to you, 'togglepr} {/if {@InList(petwars1,@CapName(@LTrim($9)))==1} {/if {@GetArray(petwars,@Var(x@CapName(@LTrim($9))),17)==1} {/assign {petwars} {@Var(x@CapName(@LTrim($9))),17} {0};/emote @LTrim($9) Your prompt has been turned off} {/assign {petwars} {@Var(x@CapName(@LTrim($9))),17} {1};/emote @LTrim($9) Your prompt has been turned on}}} {/emote @LTrim($9) You need to @ForeCyan()create@ForeRed() a pet first}} {Petwars}
/action {^<CHAT> %2 is now %3.} {/var chatwho $3;/chat $chatwho Changing your chat name will result in disconnection from the server. Please connect under the name you wish to use;/unchat $chatwho} {Petwars}
/action {Chat connection estab} {/chatserv {@Var(whoconnect)};/itemadd {petwars2} {@CapName(@Var(whoconnect))};/chat @Var(whoconnect) Chat to me 'help' if this is your first time here;/roomall @AnsiBold()@ForeCyan()@CapName(@Var(whoconnect)) @ForeMagenta()has joined the madness!} {Petwars}
/action {Chat request from %5 accepted.} {/var {whoconnect} {$5}} {Petwars}

/var {petbattle0} {0} {Petwars}
/var {petbattle2} {0} {Petwars}
/var {petbattle0mess} {-} {Petwars}
/var {petbattle2mess} {-} {Petwars}

/event {battle} {3} {checkbattles} {Petwars}
/event {checkqueue} {10} {/if {@Var(petbattle0)==0} {loadbattle 0} {/if {1=2} {/if {@Var(petbattle2)==0} {loadbattle 2} {}} {}}} {Petwars}

/alias {loadbattle %1} {/if {@GetCount(queue)>0} {/if {@GetArray(petwars,@Var(x@Word(@GetItem(queue,1),2)),20)>0 && @GetArray(petwars,@Var(x@Word(@GetItem(queue,1),3)),20)>0} {setpets $1;/itemdelete {queue} {1};startbattle $1} {/roomall @AnsiBold()@ForeYellow()The battle with @Word(@GetItem(queue,1),2) and @Word(@GetItem(queue,1),3) has been cancelled;/itemdelete queue 1}} {}} {Petwars}
/alias {setpets %2} {/var {x1} {@Math($2+1)};/var {x2} {@Math($2+2)};/var {pet@Var(x1)} {@Word(@GetItem(queue,1),2)};/var {pet@Var(x2)} {@Word(@GetItem(queue,1),3)};/var {pet@Var(x1)hp} {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x1)))),5)};/var {pet@Var(x2)hp} {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x2)))),5)};/var {pet@Var(x1)mana} {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x1)))),6)};/var {pet@Var(x2)mana} {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x2)))),6)};/var {pet@Var(x1)sanc} {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x1)))),22)};/var {pet@Var(x1)striking} {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x1)))),23)};/var {pet@Var(x2)sanc} {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x2)))),22)};/var {pet@Var(x2)striking} {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x2)))),23)};/var {pet@Var(x1)lag} {0};/var {pet@Var(x2)lag} {0};/var {pet@Var(x1)cursed} {0};/var {pet@Var(x2)cursed} {0}} {Petwars}
/alias {checkbattles} {/if {@Var(petbattle0)} {/empty {petbattle0mess};dopet 1;dopet 2;showhps 1;showhps 2;/if {@Var(petbattle@Var(petbattle))} {/roomall @Var(petbattle0mess);prompt 1;prompt 2} {}} {};/if {@Var(petbattle2)==1} {/empty {petbattle2mess};dopet 3;dopet 4;showhps 3;showhps 4;/if {@Var(petbattle@Var(petbattle))} {/roomall @Var(petbattle2mess);prompt 3;prompt 4} {}}} {Petwars}
/alias {startbattle %2} {/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),4)>1} {/var {pet@Var(x1)weapon} {'s pierce}} {/empty {pet@Var(x1)weapon}};/if {@GetArray(petwars,@Var(x@Var(pet@Var(x2))),4)>1} {/var {pet@Var(x2)weapon} {'s pierce}} {/empty pet@Var(x2)weapon};/var {petbattle$2} {1};/roomall @AnsiBold()@ForeYellow()The battle has begun!;checkbs @Var(pet@Var(x1));/fireev {battle}} {Petwars}
/alias {prompt %0} {/if {@GetArray(petwars,@Var(x@CapName(@Var(pet$0))),17)==1} {/emote @Var(pet$0) @AnsiBold()@ForeBlue()<@ForeCyan()@Var(pet$0hp)@ForeBlue()hp @ForeMagenta()@Var(pet$0mana)@ForeBlue()mn>} {}} {Petwars}
/alias {dopet %0} {/var {x1} {$0};/if {$0==1} {/var {x2} {2};/var {petbattle} {0}} {/if {$0==2} {/var {x2} {1}} {/if {$0==3} {/var {x2} {4};/var {petbattle} {2}} {/var {x2} {3}}}};petcond $0;petattack @Random(@Math(200+(30*@Var(pet@Var(x1)striking))));/loop {1,2} {/if {@Math(((@GetArray(petwars,@Var(x@Var(pet@Var(x1))),13)-9)4)+@Random(26)+@Random(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),8)))>@Math(40+($LoopCount*14))} {petattack @Random(@Math(200-($LoopCount*4)+(30*@Var(pet@Var(x1)striking))))} {}};/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),24)==1 || @GetArray(petwars,@Var(x@Var(pet$0)),25)==1} {/if {@Math(((@GetArray(petwars,@Var(x@Var(pet@Var(x1))),13)-9)3)+@Random(26)+@Random(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),8)))>75} {petattack @Random(@Math(188-(30*@Var(pet@Var(x1)striking))))} {}} {};/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),3)==1} {/if {@Math(((@GetArray(petwars,@Var(x@Var(pet@Var(x1))),13)-10)3)+@Random(26)+@Random(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),8)))>82} {petattack @Random(@Math(184+(30*@Var(pet@Var(x1)striking))))} {}} {};/if {@Var(pet@Var(x1)striking)>0} {petattack @Random(188)} {};/if {@Var(petbattle@Var(petbattle))} {special@GetArray(petwars,@Var(x@Var(pet@Var(x1))),3)} {}} {Petwars}
/alias {petcond %3} {/var {pet$3condx} {@MathFloat(@MathFloat(@Var(pet$3hp)/@GetArray(petwars,@Var(x@CapName(@Var(pet$3))),5))*100)};/if {@Var(pet$3condx)>0} {/var {pet$3cond} {@GetArray(health,@Var(pet$3condx),1)}} {/if {@Var(pet$3condx)<0} {/var {pet$3cond} {is dead.}} {/var {pet$3cond} {is stunned.}}}} {Petwars}

/alias {petattack %4} {/var {roll} {$4};/if {@Var(petbattle@Var(petbattle))} {docalchit;/if {@Random(20)>19} {dopetattack} {/if {@Var(roll) > @Var(calchit)} {/if {@Var(combatdebug)} {/showme {@AnsiBold()@ForeWhite()roll is at@ForeBlue(): @ForeCyan()@Var(roll)@Chr(10)@ForeWhite()calchit at@ForeBlue(): @ForeCyan()@Var(calchit) @ForeGreen()(hitting)}} {};dopetattack} {/if {@Var(combatdebug)} {/showme {@AnsiBold()@ForeWhite()roll is at@ForeBlue(): @ForeCyan()@Var(roll)@Chr(10)@ForeWhite()calchit at@ForeBlue(): @ForeCyan()@Var(calchit) @ForeGreen()(missing)}} {};dopetmiss}}}} {}} {Petwars}

/alias {docalchit} {/var {calchit} {@Math(200-(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),2)*@Var(clhit@GetArray(petwars,@Var(x@Var(pet@Var(x1))),3))))};/var {calchit} {@Math(@Var(calchit)-((@GetArray(petwars,@Var(x@Var(pet@Var(x1))),10)-10)*2))};/var {calchit} {@MathFloat(@Var(calchit)-(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),8)*.7))};/var {calchit} {@MathFloat(@Var(calchit)-@GetArray(petwars,@Var(x@Var(pet@Var(x2))),7))}} {Petwars}
/alias {dopetattack %5} {/if {@Var(petbattle@Var(petbattle))==1} {getpetdam}} {Petwars}
/alias {getpetdam} {/if {@Var(petbattle@Var(petbattle))} {petweapondam;/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),3)==1 || @GetArray(petwars,@Var(x@Var(pet@Var(x1))),3)==2} {/var {drbon} {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),9)}} {/var {drbon} {@Random(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),9))}};/if {@Var(petbattle@Var(petbattle))==1} {/var {petdam} {@Math(@Var(petweapdam)+@Var(drbon))};/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),3)==1 && @Random(50)>48} {/var {petdam} {@Math(2*@Var(petdam))};battlemess @AnsiBold()@ForeRed()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x1)))),1) critically hits @Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1)!} {};/if {@Var(pet@Var(x2)sanc)==1} {/var {petdam} {@Math(@Var(petdam)/2)}} {};damage @Var(petdam);/if {$damx} {petkill @AnsiBold()@ForeGreen()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1)@Var(pet@Var(x1)weapon) @ForeRed()kills @ForeGreen()@Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1)!} {petdammess;/var {pet@Var(x2)hp} {@Math(@Var(pet@Var(x2)hp)-@Var(petdam))}}} {}} {}} {Petwars}
/alias {petweapondam} {petweap@GetArray(petwars,@Var(x@Var(pet@Var(x1))),4)} {Petwars}

/alias {battlemess %6} {/if {@IsEmpty(petbattle@Var(petbattle)mess)==1} {/var {petbattle@Var(petbattle)mess} {$6}} {/var {petbattle@Var(petbattle)mess} {@ConCat(@LTrim(@Var(petbattle@Var(petbattle)mess)),@Chr(10)$6)}}} {Petwars}

/alias {petdammess} {/if {@Var(petbattle@Var(petbattle))} {/if {@Var(petdam)>129} {/var {petdamtemp} {viciously rends}} {/var {petdamtemp} {@GetArray(damage,@Var(petdam),1)}};/var {petmess} {@AnsiBold()@ForeGreen()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1)@Var(pet@Var(x1)weapon) @ForeCyan()@Var(petdamtemp) @ForeGreen()@Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x2)))),1)!};battlemess @Var(petmess)} {}} {Petwars}
/alias {dopetmiss} {/if {@Var(petbattle@Var(petbattle))} {/var {petmess} {@AnsiBold()@ForeGreen()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1)@Var(pet@Var(x1)weapon) @ForeMagenta()misses @ForeGreen()@Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1).};battlemess @Var(petmess)} {}} {Petwars}
/alias {damage %4} {/if {$4>@Math(@Var(pet@Var(x2)hp)-1)} {/var damx 1} {/var damx 0}} {Petwars}
/alias {petkill %5} {/var {petbattle@Var(petbattle)} {0};battlemess $5;battlemess @AnsiBold()@ForeRed()You cringe as @Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1) cries out in anguish.;/roomall @Var(petbattle@Var(petbattle)mess);dopetwin;dopetloss;/var {petbattle@Var(petbattle)} {0}} {Petwars}

/alias {dopetwin} {getwin;/emote @Var(pet@Var(x1)) Your pet @AnsiBold()@ForeCyan()won@ForeRed()! You get @ForeWhite()@Var(winpts) @ForeRed()pts and @ForeWhite()@GetArray(petwars,@Var(x@Var(pet@Var(x2))),2) @ForeRed()xp for your victory.;givexp;/assign {petwars} {@Var(x@Var(pet@Var(x1))),18)} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),18)+1)};/assign {petwars} {@Var(x@Var(pet@Var(x2))),19)} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x2))),19)+1)};/assign {petwars} {@Var(x@Var(pet@Var(x1))),20} {0};/assign {petwars} {@Var(x@Var(pet@Var(x2))),20} {0};/assign {petwars} {@Var(x@Var(pet@Var(x1))),22} {0};/assign {petwars} {@Var(x@Var(pet@Var(x1))),23} {0};/assign {petwars} {@Var(x@Var(pet@Var(x2))),22} {0};/assign {petwars} {@Var(x@Var(pet@Var(x2))),23} {0};/assign {petwars} {@Var(x@Var(pet@Var(x1))),16} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),16)+@Var(winpts))};/assign {petwars} {@Var(x@Var(pet@Var(x2))),16} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x2))),16)+4)};/emote @Var(pet@Var(x2)) Your pet has @AnsiBold()@ForeYellow()lost@ForeRed(), but you received @ForeWhite()4 @ForeRed()pts for your effort.} {Petwars}
/alias {getwin} {/var {winpts} {@Math(5+@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x2))),2)-@GetArray(petwars,@Var(x@Var(pet@Var(x1))),2)))};/if {@Var(winpts)>10} {/var {winpts} {10}} {};/if {@Var(winpts)<1} {/var {winpts} {1}} {}} {Petwars}
/alias {givexp} {/assign {petwars} {@Var(x@Var(pet@Var(x1))),15} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),15)+@GetArray(petwars,@Var(x@Var(pet@Var(x2))),2))};checkpetlevel} {Petwars}
/alias {checkpetlevel} {/var {tolevel} {@Pow(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),2),2)};/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),2)<25} {/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),3)<1} {/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),15)>=@Math(@Var(tolevel)+@GetArray(petwars,@Var(x@Var(pet@Var(x1))),2)-1)} {dolevel} {}} {/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),15)>=@Math(@Var(tolevel)+(5*(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),2)-1)))} {dolevel} {}}} {/assign {petwars} {@Var(x@Var(pet@Var(x1))),15} {0}}} {Petwars}
/alias {dolevel} {dogains;/emote @Var(pet@Var(x1)) Your pet has @AnsiBold()@ForeCyan()leveled@ForeRed()! It's gains are: @Var(hpgain)hp/@Var(managain)mana @Var(hrgain)hr/@Var(drgain)dr @Math(@Var(ptgain)+2)pts} {Petwars}
/alias {dogains} {/if {@GetArray(petwars,@Var(x@Var(pet@Var(x1))),3)==0} {/var {hpgain} {@Var(con@GetArray(petwars,@Var(x@CapName(@Var(pet1))),14))}} {/var {hpgain} {@Var(rcon@GetArray(petwars,@Var(x@CapName(@Var(pet1))),14))}};/var {managain} {@Var(int@GetArray(petwars,@Var(x@Var(pet@Var(x1))),12))};/var {drgain} {@Var(str@GetArray(petwars,@Var(x@Var(pet@Var(x1))),10))};/var {hrgain} {@Var(dex@GetArray(petwars,@Var(x@Var(pet@Var(x1))),13))};/var {ptgain} {@Var(wis@GetArray(petwars,@Var(x@Var(pet@Var(x1))),11))};/assign {petwars} {@Var(x@Var(pet@Var(x1))),2} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),2)+1)};/assign {petwars} {@Var(x@Var(pet@Var(x1))),5} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),5)+@Var(hpgain))};/assign {petwars} {@Var(x@Var(pet@Var(x1))),6} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),6)+@Var(managain))};/assign {petwars} {@Var(x@Var(pet@Var(x1))),8} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),8)+@Var(hrgain))};/assign {petwars} {@Var(x@Var(pet@Var(x1))),9} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),9)+@Var(drgain))};/assign {petwars} {@Var(x@Var(pet@Var(x1))),15} {0};/assign {petwars} {@Var(x@Var(pet@Var(x1))),16} {@Math(@GetArray(petwars,@Var(x@Var(pet@Var(x1))),16)+@Math(@Var(ptgain)+2))};checkstat @Var(pet@Var(x1)) hp;checkstat @Var(pet@Var(x1)) mana;checkstat @Var(pet@Var(x1)) hr;checkstat @Var(pet@Var(x1)) dr} {Petwars}

/alias {addpetwars %0} {/itemadd {petwars2} {$0}} {Petwars}
/alias {addstat %0} {/assign {petwars} {@Var(x@CapName(@Word($0,1))),16} {@Math(@GetArray(petwars,@Var(x@CapName(@Word($0,1))),16)-@Math(@Var(stco@Word($0,2))*@Word($0,3)))};/assign {petwars} {@Var(x@CapName(@Word($0,1))),@Var(@Word($0,2)arr)} {@Math(@GetArray(petwars,@Var(x@CapName(@Word($0,1))),@Var(@Word($0,2)arr))+@Word($0,4))};/emote @Word($0,1) Your pet's @Word($0,2) has increased @Word($0,3) time(s) to @GetArray(petwars,@Var(x@CapName(@Word($0,1))),@Var(@Word($0,2)arr))} {Petwars}
/alias {checkaccept %4} {/if {@GetArray(petwars,@Var(x$4),20)==2 && @GetArray(petwars,@Var(x@GetArray(petwars,@Var(x$4),21)),20)==1} {/assign {petwars} {@Var(x$4),20} {3};/emote $4 OK, you have accepted the challenge, you are now in the queue;/emote @GetArray(petwars,@Var(x$4),21) $4 has accepted your challenge, you are now in the queue;getqnum;/if {@Random(2)==1} {/itemadd {queue} {@Var(qnum) $4 @GetArray(petwars,@Var(x$4),21)}} {/itemadd {queue} {@Var(qnum) @GetArray(petwars,@Var(x$4),21) $4}}} {/assign {petwars} {@Var(x$4),20} {0};/emote $4 Either you are not being challenged, or your challenger has declined}} {Petwars}
/alias {checkbs} {/if {@GetArray(petwars,@Var(x@CapName(@Var(pet@Var(x1)))),3)==2 && @GetArray(petwars,@Var(x@CapName(@Var(pet1))),4)>1} {dobs} {}} {Petwars}

/alias {checkchallenge %3} {/if {"@Word($3,1)"!="@Word($3,2)"} {checkpet} {/emote @Word($3,1) You may not challenge yourself}} {Petwars}
/alias {checkpet} {/if {@InList(petwars1,@Word($3,1))==1} {checkchallenge1} {/emote @Word($3,1) You do not have a pet!}} {Petwars}
/alias {checkchallenge1} {/if {@InList(petwars2,@Word($3,2))==1 && @InList(petwars1,@Word($3,2))==1} {checklevel} {/emote @Word($3,1) Your opponent is not connected, or your opponent does not have a pet}} {Petwars}
/alias {checklevel} {/if {@Abs(@Math(@GetArray(petwars,@Var(x@Word($3,1)),2)-@GetArray(petwars,@Var(x@Word($3,2)),2)))<6 && @InList(petwars2,@Word($3,2))==1} {checkchallenge2} {/emote @Word($3,1) @AnsiBold()@ForeRed()The level difference between you and @ForeCyan()@Word($3,2) @ForeRed()is too great.}} {Petwars}
/alias {checkchallenge2} {/if {@InList(queue,@Word($3,1))!=1 && @InList(queue,@Word($3,2))!=1} {checkchallenge3} {/emote @Word($3,1) Either your or your opponent is already in the queue.}} {Petwars}
/alias {checkchallenge3} {/if {@GetArray(petwars,@Var(x@Word($3,1)),20)==0 && @GetArray(petwars,@Var(x@Word($3,2)),20)==0} {initchallenge @Word($3,1) @Word($3,2);sendchallenge} {checkdeny1}} {Petwars}
/alias {initchallenge %4} {/assign {petwars} {@Var(x@Word($4,1)),20} {1};/assign {petwars} {@Var(x@Word($4,2)),20} {2};/assign {petwars} {@Var(x@Word($4,1)),21} {@Word($4,2)};/assign {petwars} {@Var(x@Word($4,2)),21} {@Word($4,1)}} {Petwars}
/alias {checkdeny1} {/if {@GetArray(petwars,@Var(x@Word($3,1)),20)==1} {/emote @Word($3,1) @AnsiBold()You are already challenging @ForeCyan()@GetArray(petwars,@Var(x@Word($3,1)),21)} {checkdeny2}} {Petwars}
/alias {checkdeny2} {/if {@GetArray(petwars,@Var(x@Word($3,1)),20)==2} {/emote @Word($3,1) @AnsiBold()You are already being challenged by @ForeCyan()@GetArray(petwars,@Var(x@Word($3,1)),21)} {checkdeny3}} {Petwars}
/alias {checkdeny3} {/if {@GetArray(petwars,@Var(x@Word($3,2)),20)==1} {/emote @Word($3,1) @AnsiBold()@ForeCyan()@Word($3,2) @ForeRed()is already being challenged} {checkdeny4}} {Petwars}
/alias {checkdeny4} {/if {@GetArray(petwars,@Var(x@Word($3,2)),20)==1} {/emote @Word($3,1) @AnsiBold()@ForeCyan()@Word($3,2) @ForeRed()is already challenging someone} {}} {Petwars}

/alias {sendchallenge} {/emote @Word($3,1) @AnsiBold()@ForeRed()Asking @ForeCyan()@Word($3,2) @ForeRed()to battle...;/emote @Word($3,2) @AnsiBold()@ForeCyan()@Word($3,1)@ForeBlue()[@ForeGreen()L@GetArray(petwars,@Var(x@Word($3,1)),2)@ForeBlue()] @ForeRed()wants to battle! Chat to me 'accept' to battle.} {Petwars}

/alias {checkincrease %7} {/if {@WordCount($7)==2 && @Abs(@Math(@GetArray(petwars,@Var(x@CapName(@LTrim($0))),@Var(@Word($7,1)arr))+@Math(@Word($7,2)*@Var(add@Word($7,1)))))<@Abs(@Var(@Word($7,1)max))} {/if {@Word($7,2)>=1} {/if {@GetArray(petwars,@Var(x@CapName(@LTrim($0))),16)>=@Math(@Var(stco@Word($7,1))*@Word($7,2))} {addstat @CapName(@LTrim($0)) @Word($7,1) @Word($7,2) @Math(@Var(add@Word($7,1))*@Word($7,2))} {/emote @LTrim($0) You do not have enough points for that increase.}} {/emote @LTrim($0) Increase must be above 0.}} {/emote @LTrim($0) To raise your pet's stats use increase <stat> <how many times>}} {Petwars}
/alias {checkacincrease %7} {/if {@Math(@GetArray(petwars,@Var(x@CapName(@LTrim($0))),@Var(acarr))+@Math($7*@Var(addac)))>=@Math(100-(@GetArray(petwars,@Var(x@CapName(@LTrim($0))),2)*10))} {/if {$7>=1} {/if {@GetArray(petwars,@Var(x@CapName(@LTrim($0))),16)>=@Math(@Var(stcoac)*$7)} {addstat @CapName(@LTrim($0)) ac $7 @Math(@Var(addac)*$7)} {/emote @LTrim($0) You do not have enough points for that increase.}} {/emote @LTrim($0) Increase must be above 0.}} {/emote @LTrim($0) Your pet's @AnsiBold()@ForeCyan()AC @ForeRed()cannot be improved below @ForeCyan()@Math(100-(@GetArray(petwars,@Var(x@CapName(@LTrim($0))),2)*10))@AnsiBold()@ForeRed()}} {Petwars}

/alias {checkinlist %0} {/if {@InList(petwars1,$0)==1} {/emote $0 If you would like to lose your current pet, try @AnsiBold()@ForeCyan()reset pet@ForeRed()} {makepet $0}} {Petwars}

/alias {checklevel2} {/if {@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2)<21} {/if {"@GetArray(petwars,@Var(x@CapName(@Var(pet2))),3)"=="none"} {/if {@GetArray(petwars,@Var(x@CapName(@Var(pet2))),15)>=@Math(@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2)*@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2))+@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2))} {dolevel2} {}} {/if {@GetArray(petwars,@Var(x@CapName(@Var(pet2))),15)>=@Math(@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2)*@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2))+@Math(5*@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2)-1)))} {dolevel2} {}}} {/assign {petwars} {@Var(x@CapName(@Var(pet2))),15} {0}}} {Petwars}

/alias {checkstat %6} {/if {@GetArray(petwars,@Var(x@Word($6,1)),@Var(@Word($6,2)arr))>@Var(@Word($6,2)max)} {/assign {petwars} {@Var(x@Word($6,1)),@Var(@Word($6,2)arr)} {@Var(@Word($6,2)max)}} {}} {Petwars}

/alias {dobs} {/var {acbon} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),7)/10)} {Petwars};/if {@Math(@Math(@Var(acbon)+@Random(20))+@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),8)/10))>=@Math(6-@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet1))),13)-@GetArray(petwars,@Var(x@CapName(@Var(pet2))),13)))} {dohitbs} {domissbs}} {Petwars}
/alias {domissbs} {/roomall @AnsiReset()@ForeWhite()@Var(pet1)'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet1))),1) stabs at @Var(pet2)'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet2))),1) with a @Var(weap@GetArray(petwars,@Var(x@CapName(@Var(pet1))),4)) dagger, yet hits nothing but air.} {Petwars}

/alias {dogains2} {/if {"@GetArray(petwars,@Var(x@CapName(@Var(pet2))),3)"=="none"} {/var {hpgain2} {@Var(con@GetArray(petwars,@Var(x@CapName(@Var(pet2))),14))}} {/var {hpgain2} {@Var(rcon@GetArray(petwars,@Var(x@CapName(@Var(pet2))),14))}};/var {managain2} {@Var(int@GetArray(petwars,@Var(x@CapName(@Var(pet2))),12))};/var {drgain2} {@Var(str@GetArray(petwars,@Var(x@CapName(@Var(pet2))),10))};/var {hrgain2} {@Var(dex@GetArray(petwars,@Var(x@CapName(@Var(pet2))),13))};/var {ptgain2} {@Var(wis@GetArray(petwars,@Var(x@CapName(@Var(pet2))),11))};/assign {petwars} {@Var(x@CapName(@Var(pet2))),2} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2)+1)};/assign {petwars} {@Var(x@CapName(@Var(pet2))),5} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),5)+@Var(hpgain2))};/assign {petwars} {@Var(x@CapName(@Var(pet2))),6} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),6)+@Var(managain2))};/assign {petwars} {@Var(x@CapName(@Var(pet2))),8} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),8)+@Var(hrgain2))};/assign {petwars} {@Var(x@CapName(@Var(pet2))),9} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),9)+@Var(drgain2))};/assign {petwars} {@Var(x@CapName(@Var(pet2))),15} {0};/assign {petwars} {@Var(x@CapName(@Var(pet2))),16} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),16)+@Math(@Var(ptgain2)+2))};checkstat @Var(pet2) hp;checkstat @Var(pet2) mana;checkstat @Var(pet2) hr;checkstat @Var(pet2) dr} {Petwars}
/alias {dohitbs} {pet1weapondam;/var {bsdam} {@Math(@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet1))),2)/7)*@MathFloat(@Math(@Var(pet1weapondam)+@GetArray(petwars,@Var(x@CapName(@Var(pet1))),9))*@ConCat(.,@Math(7+@Random(3)))))};/if {@Var(bsdam)>@Var(pet2hp)} {/roomall @AnsiBold()@ForeRed()@Var(pet1)'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet1))),1) brutally slays @Var(pet2)'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet2))),1).;/var battle 0;dopet1win} {/roomall @AnsiBold()@ForeRed()@Var(pet1)'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet1))),1) stabs @Var(pet2)'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet2))),1) in the back with a @Var(weap@GetArray(petwars,@Var(x@CapName(@Var(pet1))),4)) dagger!;pet2damage @Var(bsdam)}} {Petwars}
/alias {dolevel2} {dogains2;/emote @Var(pet2) Your pet has @AnsiBold()@ForeCyan()leveled@ForeRed()! It's gains are: @Var(hpgain2)hp/@Var(managain2)mana @Var(hrgain2)hr/@Var(drgain2)dr @Math(@Var(ptgain2)+2)pts} {Petwars}


/alias {doreclass %5} {/emote @Word($5,1) OK, your pet has become a @AnsiBold()@ForeCyan()@Word($5,2);/assign {petwars} {@Var(x@Word($5,1)),2} {1};/assign {petwars} {@Var(x@Word($5,1)),3} {@Var(class@Word($5,2))};/assign {petwars} {@Var(x@Word($5,1)),@Var(classarr@Word($5,2))} {1};/assign {petwars} {@Var(x@Word($5,1)),4} {1};/assign {petwars} {@Var(x@Word($5,1)),5} {100};/assign {petwars} {@Var(x@Word($5,1)),6} {50};/assign {petwars} {@Var(x@Word($5,1)),7} {100};/assign {petwars} {@Var(x@Word($5,1)),8} {20};/assign {petwars} {@Var(x@Word($5,1)),9} {10};/assign {petwars} {@Var(x@Word($5,1)),10} {10};/assign {petwars} {@Var(x@Word($5,1)),11} {10};/assign {petwars} {@Var(x@Word($5,1)),12} {10};/assign {petwars} {@Var(x@Word($5,1)),13} {10};/assign {petwars} {@Var(x@Word($5,1)),14} {10};/assign {petwars} {@Var(x@Word($5,1)),15} {0};/assign {petwars} {@Var(x@Word($5,1)),16} {5};/assign {petwars} {@Var(x@Word($5,1)),17} {no};/assign {petwars} {@Var(x@Word($5,1)),18} {0};/assign {petwars} {@Var(x@Word($5,1)),19} {0};/assign {petwars} {@Var(x@Word($5,1)),20} {0};/assign {petwars} {@Var(x@Word($5,1)),21} {none}} {Petwars}
/alias {getmessages} {/empty messages;/var {messages} {@AnsiBold()@ForeRed()## @ForeCyan()Poster                     Message};/loop {1,@GetCount(messages)} {/var {messages} {@ConCat(@Var(messages),@Chr(10)@ForeRed()$LoopCount @ForeCyan()@Word(@GetItem(messages,$LoopCount),1) @ForeGreen()@Word(@GetItem(messages,$LoopCount),2) @Word(@GetItem(messages,$LoopCount),3) @Word(@GetItem(messages,$LoopCount),4) @Word(@GetItem(messages,$LoopCount),5) @Word(@GetItem(messages,$LoopCount),6))}}} {Petwars}
/alias {getpet2dam} {/if {@Var(battle)==1} {pet2weapondam;/if {@GetArray(petwars,@Var(x@CapName(@Var(pet2))),3)==1 || @GetArray(petwars,@Var(x@CapName(@Var(pet2))),3)==2} {/var {drbon2} {@GetArray(petwars,@Var(x@CapName(@Var(pet2))),9)}} {/var {drbon2} {@Random(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),9))}};/if {@Var(battle)==1} {/var {pet2dam} {@Math(@Var(pet2weapondam)+@Var(drbon2))};/if {@GetArray(petwars,@Var(x@CapName(@Var(pet2))),3)==1 && @Random(50)>49} {/var {pet2dam} {@Math(2*@Var(pet2dam))};/var {pet2battlemess} {@ConCat(@LTrim(@Var(pet2battlemess)),@Chr(10)@AnsiBold()@ForeRed()@Var(pet2)'s pet\, @GetArray(petwars,@Var(x@CapName(@Var(pet2))),1) critically hits @Var(pet1)'s pet\, @GetArray(petwars,@Var(x@CapName(@Var(pet1))),1)!)}} {};/if {@Var(pet1sanc)==1} {/var {pet2dam} {@Math(@Var(pet2dam)/2)}} {};/if {@Var(pet2dam)>@Var(pet1hp)} {pet2kill} {pet2dammess;/var {pet1hp} {@Math(@Var(pet1hp)-@Var(pet2dam))}}} {}} {}} {Petwars}
/alias {getqnum} {/math {numbattles} {$numbattles+1};/var {qnum} {@PadLeft(@Var(numbattles),0,@Math(4-@Len(@Var(numbattles))))}} {Petwars}
/alias {getqueue} {/empty queue;/var {queue} {@AnsiBold()@ForeRed()## @ForeCyan()Players};/loop {1,@GetCount(queue)} {/var {queue} {@ConCat(@Var(queue),@Chr(10)@ForeRed()$LoopCount @ForeCyan()@Word(@GetItem(queue,$LoopCount),2) @Word(@GetItem(queue,$LoopCount),3))}}} {Petwars}
/alias {getwhoison} {/empty {whoison};/var {whoison} {@AnsiBold()@ForeYellow()Player         Pet Level};/if {@GetCount(petwars2)>0} {/loop {1,@GetCount(petwars2)} {/if {@InList(petwars1,@GetItem(petwars2,$LoopCount))==1} {/var {whoison} {@ConCat(@Var(whoison),@Chr(10)@AnsiBold()@ForeCyan()@GetItem(petwars2,$LoopCount)@PadLeft(@ForeMagenta()@GetArray(petwars,@Var(x@GetItem(petwars2,$LoopCount)),2), ,@Math(15-@Len(@GetItem(petwars2,$LoopCount)))))}}} {}} {}} {Petwars}
/alias {getwin2} {/var {winpts2} {@Math(5+@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet1))),2)-@GetArray(petwars,@Var(x@CapName(@Var(pet2))),2)))};/if {@Var(winpts2)>10} {/var {winpts2} {10}} {};/if {@Var(winpts2)<1} {/var {winpts2} {1}} {}} {Petwars}
/alias {givestats %0} {/if {@GetArray(petwars,@Var(x$0),3)==0} {/var {class} {@Chr(10)@AnsiBold()@ForeGreen()Level @ForeCyan()@GetArray(petwars,@Var(x$0),2)}} {/var {class} {@AnsiBold()@ForeBlue()- };/if {@GetArray(petwars,@Var(x$0),26)} {/var {class} {@ConCat(@Var(class),@ForeYellow()C)}} {};/if {@GetArray(petwars,@Var(x$0),27)} {/var {class} {@ConCat(@Var(class),@ForeYellow()M)}} {};/if {@GetArray(petwars,@Var(x$0),25)} {/var {class} {@ConCat(@Var(class),@ForeYellow()T)}} {};/if {@GetArray(petwars,@Var(x$0),24)>0} {/var {class} {@ConCat(@Var(class),@ForeYellow()W)}} {};/var {class} {@ConCat(@Var(class)@ForeBlue()])};/var {class} {@ConCat(@Var(class),@Chr(10)@ForeGreen()Level @ForeCyan()@GetArray(petwars,@Var(x$0),2) @CapName(@Var(class@GetArray(petwars,@Var(x$0),3))))}};/if {@GetArray(petwars,@Var(x$0),20)==2} {/var {challenge} {@AnsiBold()@ForeWhite()being challenged by @ForeCyan()@GetArray(petwars,@Var(x$0),21)}} {/if {@GetArray(petwars,@Var(x$0),20)==1} {/var {challenge} {@AnsiBold()@ForeWhite()challenging @ForeCyan()@GetArray(petwars,@Var(x$0),21)}} {/var {challenge} {@AnsiBold()@ForeWhite()@Var(chal@GetArray(petwars,@Var(x$0),20))}}};/emote $0 @Chr(10)@AnsiBold()@ForeCyan()@GetArray(petwars,@Var(x@CapName($0)),1) @Var(class)@Chr(10)@ForeYellow()Exp Pts Hp    Mana  AC    Wins Losses@Chr(10)@AnsiBold()@ForeBlue()@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196) @Chr(10)@AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@CapName($0)),15), ,@Math(4-@Len(@GetArray(petwars,@Var(x@CapName($0)),15))))@PadRight(@GetArray(petwars,@Var(x@CapName($0)),16), ,@Math(4-@Len(@GetArray(petwars,@Var(x@CapName($0)),16))))@PadRight(@GetArray(petwars,@Var(x@CapName($0)),5), ,@Math(5-@Len(@GetArray(petwars,@Var(x@CapName($0)),5)))) @PadRight(@GetArray(petwars,@Var(x@CapName($0)),6), ,@Math(5-@Len(@GetArray(petwars,@Var(x@CapName($0)),6)))) @PadRight(@GetArray(petwars,@Var(x@CapName($0)),7), ,@Math(4-@Len(@GetArray(petwars,@Var(x@CapName($0)),7))))  @PadRight(@GetArray(petwars,@Var(x@CapName($0)),18), ,@Math(4-@Len(@GetArray(petwars,@Var(x@CapName($0)),18)))) @PadRight(@GetArray(petwars,@Var(x@CapName($0)),19), ,@Math(4-@Len(@GetArray(petwars,@Var(x@CapName($0)),19))))@Chr(10)@AnsiBold()@ForeYellow()Hr  Dr  Str Wis Int Dex Con  Weapon@Chr(10)@AnsiBold()@ForeBlue()@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(10)@AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@CapName($0)),8), ,@Math(3-@Len(@GetArray(petwars,@Var(x@CapName($0)),8)))) @AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@CapName($0)),9), ,@Math(3-@Len(@GetArray(petwars,@Var(x@CapName($0)),9)))) @GetArray(petwars,@Var(x@CapName($0)),10)  @GetArray(petwars,@Var(x@CapName($0)),11)  @GetArray(petwars,@Var(x@CapName($0)),12)  @ForeCyan()@GetArray(petwars,@Var(x@CapName($0)),13)  @ForeCyan()@GetArray(petwars,@Var(x@CapName($0)),14)   @Var(weap@GetArray(petwars,@Var(x@CapName($0)),4))@Chr(10)@ForeRed()Your current challenge status is@ForeBlue(): @ForeWhite()@Var(challenge)@Chr(10)@AnsiBold()@ForeWhite()Your current prompt setting is@ForeBlue(): @ForeCyan()@Var(prompt@GetArray(petwars,@Var(x@CapName($0)),17))} {Petwars}
/alias {givexp2} {/assign {petwars} {@Var(x@CapName(@Var(pet2))),15} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),15)+@GetArray(petwars,@Var(x@CapName(@Var(pet1))),2))};checklevel2} {Petwars}

/alias {makehtml} {/filedelete {pethtml.html};/calldll FileLog.dll Open {1 pethtml.html};/loop {1,@GetCount(petwars1)} {/calldll FileLog.dll Write {1 @GetItem(petwars1,$LoopCount): @Chr(10)@AnsiBold()@ForeCyan()@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),1)@Chr(10)@ForeGreen()Level @ForeCyan()@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),2) @ForeGreen()Class@ForeBlue():@ForeCyan()@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),3) @ForeGreen()Weapon@ForeBlue():@ForeCyan()@Var(weap@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),4))@Chr(10)@ForeYellow()Exp Pts Hp    Mana  AC@Chr(10)@AnsiBold()@ForeBlue()@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196) @Chr(10)@AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),15), ,@Math(3-@Len(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),15)))) @PadRight(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),16), ,@Math(3-@Len(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),16)))) @PadRight(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),5), ,@Math(5-@Len(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),5)))) @PadRight(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),6), ,@Math(5-@Len(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),6)))) @PadRight(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),7), ,@Math(4-@Len(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),7))))@Chr(10)@AnsiBold()@ForeYellow()Hr  Dr  Str Wis Int Dex Con@Chr(10)@AnsiBold()@ForeBlue()@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(10)@AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),8), ,@Math(3-@Len(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),8)))) @AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),9), ,@Math(3-@Len(@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),9)))) @GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),10)  @GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),11)  @GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),12)  @ForeCyan()@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),13)  @ForeCyan()@GetArray(petwars,@Var(x@GetItem(petwars1,$LoopCount)),14)@Chr(10)@ForeRed()Your current challenge status is@ForeBlue(): @ForeWhite()@Var(chal@GetArray(petwars,@Var(x@CapName($0)),20))}}} {Petwars}
/alias {makepet %0} {/emote $0 OK, you now have a pet. Name it with name <name>;/itemadd {petwars1} {@RTrim(@LTrim($0))};/itemadd {petwars2} {@RTrim(@LTrim($0))};/var {@ConCat(x,$0)} {@GetCount(petwars1)} {Petwars};/assign {petwars} {@Var(x$0),1} {NoName};/assign {petwars} {@Var(x$0),2} {1};/assign {petwars} {@Var(x$0),3} {0};/assign {petwars} {@Var(x$0),24} {0};/assign {petwars} {@Var(x$0),25} {0};/assign {petwars} {@Var(x$0),26} {0};/assign {petwars} {@Var(x$0),27} {0};/assign {petwars} {@Var(x$0),4} {1};/assign {petwars} {@Var(x$0),5} {100};/assign {petwars} {@Var(x$0),6} {50};/assign {petwars} {@Var(x$0),7} {100};/assign {petwars} {@Var(x$0),8} {20};/assign {petwars} {@Var(x$0),9} {10};/assign {petwars} {@Var(x$0),10} {10};/assign {petwars} {@Var(x$0),11} {10};/assign {petwars} {@Var(x$0),12} {10};/assign {petwars} {@Var(x$0),13} {10};/assign {petwars} {@Var(x$0),14} {10};/assign {petwars} {@Var(x$0),15} {0};/assign {petwars} {@Var(x$0),16} {5};/assign {petwars} {@Var(x$0),17} {1};/assign {petwars} {@Var(x$0),18} {0};/assign {petwars} {@Var(x$0),19} {0};/assign {petwars} {@Var(x$0),20} {0};/assign {petwars} {@Var(x$0),22} {0};/assign {petwars} {@Var(x$0),23} {0};/assign {petwars} {@Var(x$0),21} {none};/loop {1,30} {/assign {petprof} {@Var(x$0),$LoopCount} {1}};/emote $0 Use stats to see your pet's stats.} {Petwars}
/alias {pet1damage %4} {/if {$4>@Var(pet1hp)} {dopet2win} {/var {pet1hp} {@Math(@Var(pet1hp)-$4)}}} {Petwars}
/alias {pet1healhp %3} {/var {pet1hp} {@Math(@Var(pet1hp)+$3)}} {Petwars}

/alias {hasweapon %9} {/if {@GetArray(petwars,@Var(x$9),4)>1} {/var x 1} {/var x 0}} {Petwars}
/alias {petweap1} {/var {petweapdam} {@Math(@Random(2)+@Random(2)+@Random(2)+@Random(2))}} {Petwars}
/alias {petweap2} {/var {petweapdam} {@Math(@Random(5)+@Random(5)+@Random(5)+@Random(5)+@Random(5))}} {Petwars}
/alias {petweap3} {/var {petweapdam} {@Math(@Random(4)+@Random(4)+@Random(4)+@Random(4)+@Random(4)+@Random(4)+@Random(4)+@Random(4))}} {Petwars}
/alias {petweap4} {/var {petweapdam} {@Math(@Random(6)+@Random(6)+@Random(6)+@Random(6)+@Random(6)+@Random(6)+@Random(6)+@Random(6))}} {Petwars}
/alias {petweap5} {/var {petweapdam} {@Math(@Random(8)+@Random(8)+@Random(8)+@Random(8)+@Random(8)+@Random(8)+@Random(8)+@Random(8))}} {Petwars}
/alias {petweap6} {/var {petweapdam} {@Math(@Random(8)+@Random(8)+@Random(8)+@Random(8)+@Random(8)+@Random(8)+@Random(8)+@Random(8))}} {Petwars}
/alias {petweap7} {/var {petweapdam} {@Math(@Random(10)+@Random(10)+@Random(10)+@Random(10)+@Random(10)+@Random(10)+@Random(10)+@Random(10)+@Random(10))}} {Petwars}

/alias {pet1weapnone} {/var {pet1weapondam} {@Math(@Random(4)+@Random(4))}} {Petwars}
/alias {pet1weapondam} {pet1weap@GetArray(petwars,@Var(x@CapName(@Var(pet1))),4)} {Petwars}
/alias {pet2attack %5} {/var {acbon2} {@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet1))),7)/5)};/if {@Var(battle)==1} {/if {@Random(20)>17} {dopet2attack} {/if {@Math(@Math(@Math(@Var(acbon2)+@Random(40))+@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),8)/5))+@Math(@GetArray(petwars,@Var(x@CapName(@Var(pet2))),13)/2))>=$5} {dopet2attack} {dopet2miss}}} {}} {Petwars}
/alias {pet2cond} {/var {pet2condx} {@MathFloat(@MathFloat(@Var(pet2hp)/@GetArray(petwars,@Var(x@CapName(@Var(pet2))),5))*100)};/if {@Var(pet2condx)>-1} {/var {pet2cond} {is dead.}} {};/if {@Var(pet2condx)>0} {/var {pet2cond} {barely clings to life.}} {};/if {@Var(pet2condx)>7} {/var {pet2cond} {pales visibly as death nears.}} {};/if {@Var(pet2condx)>14} {/var {pet2cond} {is covered with blood from oozing wounds.}} {};/if {@Var(pet2condx)>21} {/var {pet2cond} {has many grievous wounds.}} {};/if {@Var(pet2condx)>28} {/var {pet2cond} {looks pretty awful.}} {};/if {@Var(pet2condx)>35} {/var {pet2cond} {has some large, gaping wounds.}} {};/if {@Var(pet2condx)>40} {/var {pet2cond} {is vomiting blood.}} {};/if {@Var(pet2condx)>48} {/var {pet2cond} {grimaces with pain.}} {};/if {@Var(pet2condx)>54} {/var {pet2cond} {has quite a few wounds.}} {};/if {@Var(pet2cond)x>61} {/var {pet2cond} {winces in pain.}} {};/if {@Var(pet2condx)>68} {/var {pet2cond} {has winor wounds.}} {};/if {@Var(pet2condx)>75} {/var {pet2cond} {has some small wounds and bruises.}} {};/if {@Var(pet2condx)>82} {/var {pet2cond} {has a nasty looking welt on the forehead.}} {};/if {@Var(pet2condx)>89} {/var {pet2cond} {has a few scratches on its forehead.}} {};/if {@Var(pet2condx)>99} {/var {pet2cond} {is in excellent condition.}} {}} {Petwars}
/alias {pet2damage %4} {/if {$4>@Var(pet2hp)} {dopet1win} {/var {pet2hp} {@Math(@Var(pet2hp)-$4)}}} {Petwars}
/alias {pet2dammess} {/if {@Var(battle)==1} {/if {@Var(pet2dam)>130} {/var {pet2damtemp} {viciously rends}} {/var {pet2damtemp} {@Var(dammess@Var(pet2dam))}};/var {pet2mess} {@AnsiBold()@ForeGreen()@Var(pet2)'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet2))),1)@Var(pet2weapon) @ForeCyan()@Var(pet2damtemp) @ForeGreen()@Var(pet1)'s pet, @GetArray(petwars,@Var(x@CapName(@Var(pet1))),1)!};/if {@IsEmpty(pet2battlemess)==1} {/var {pet2battlemess} {@Var(pet2mess)}} {/var {pet2battlemess} {@ConCat(@LTrim(@Var(pet2battlemess)),@Chr(10)@Var(pet2mess))}}} {}} {Petwars}
/alias {pet2healhp %3} {/var {pet2hp} {@Math(@Var(pet2hp)+$3)}} {Petwars}
/alias {sarange %0} {/showme {@AnsiBold()@ForeWhite()ShowArray: @ForeGreen()@Word($0,1)  @ForeBlue()Showing Row(s) @ForeCyan()@Word($0,2)@ForeBlue()-@ForeCyan()@Word($0,3) @ForeBlue()and Column(s) @ForeCyan()@Word($0,4)@ForeBlue()-@ForeCyan()@Word($0,5)@AnsiReset()};/loop {@Word($0,2),@Word($0,3),LoopOne} {/showme {@PadLeft(-,-,78)};/loop {@Word($0,4),@Word($0,5),LoopTwo} {/showme {@AnsiBold()@ForeBlue()[@ForeCyan()$LoopOne@ForeBlue(),@ForeCyan()$LoopTwo@ForeBlue()] @AnsiReset()@GetArray(@Word($0,1),$LoopOne,$LoopTwo)}}}} {ShowArray2}

/alias {createpet %3} {/if {@WordCount($3)<2} {/showme {@AnsiBold()@ForeGreen()Syntax: @ForeRed()createpet [name] [class number]} {/itemadd {petwars2} {@Word($3,1)};makepet @Word($3,1);setgodmode $3}} {Petwars}
/alias {setbattle %4} {/if {@InList(petwars1,@Word($4,1))==1 && @InList(petwars1,@Word($4,2))==1} {getqnum;/assign {petwars} {@Var(x@Word($4,1)),20)} {1};/assign {petwars} {@Var(x@Word($4,2)),20)} {2};/showme {@AnsiBold()@ForeYellow()@Word($4,1) and @Word($4,2) have been added to the queue.};/if {@Random(2)==1} {/itemadd {queue} {@Var(qnum) @Word($4,1) @Word($4,2)}} {/itemadd {queue} {@Var(qnum) @Word($4,2) @Word($4,1)}}} {/showme {@AnsiBold()@ForeYellow()Player names invalid}}} {Petwars}
/alias {setgodmode %2} {/if {@InList(petwars1,@Word($2,1))==1} {setpet @Word($2,1) hp 10000;setpet @Word($2,1) mana 5000;setpet @Word($2,1) hr 100;setpet @Word($2,1) dr 100;setpet @Word($2,1) ac -100;setpet @Word($2,1) weapon 7;setpet @Word($2,1) class @Word($2,2);setpet @Word($2,1) str 18;setpet @Word($2,1) wis 18;setpet @Word($2,1) int 18;setpet @Word($2,1) dex 18;setpet @Word($2,1) con 18;setpet @Word($2,1) level 21} {}} {Petwars}
/alias {setname %0} {/assign {petwars} {@Var(x@Word($0,1)),1} {@Word($0,2)};/emote @Word($0,1) Your pet's name is now @Word($0,2)} {Petwars}
/alias {setnewbmode %2} {/if {@InList(petwars1,$2)==1} {setpet $2 hp 50;setpet $2 hr 0;setpet $2 dr 0;setpet $2 ac 100;setpet $2 weapon 1;/assign {petwars} {@Var(x$2),2} {1};/assign {petwars} {@Var(x$2),15} {0};/assign {petwars} {@Var(x$2),16} {5};/assign {petwars} {@Var(x$2),10} {10};/assign {petwars} {@Var(x$2),11} {10};/assign {petwars} {@Var(x$2),12} {10};/assign {petwars} {@Var(x$2),13} {10};/assign {petwars} {@Var(x$2),14} {10}} {}} {Petwars}
/alias {setpet %1} {/if {@InList(petwars1,@CapName(@Word($1,1)))==1 && @InList(stco,@Word($1,2))==1} {/assign {petwars} {@Var(x@CapName(@Word($1,1))),@Var(@Word($1,2)arr)} {@Word($1,3)};/showme {@AnsiBold()@ForeYellow()SetPet @ForeMagenta()Set @CapName(@Word($1,1))@ForeMagenta()'s @ForeBlue()[@ForeRed()@Word($1,2)@ForeBlue()] @ForeMagenta()to @ForeBlue()[@ForeGreen()@Word($1,3)@ForeBlue()]}} {/showme {@AnsiBold()@ForeYellow()SetPet @ForeRed()Player name or stat is invalid}}} {Petwars}
/alias {setstat %1} {/if {@InList(petwars1,@CapName(@Word($1,1)))==1} {/assign {petwars} {@Var(x@CapName(@Word($1,1))),@Word($1,2)} {@Word($1,3)};/showme {@AnsiBold()@ForeYellow()SetPet @ForeMagenta()Set slot @Word($1,2) to @ForeBlue()[@ForeRed()@Word($1,3)@ForeBlue()] @ForeMagenta()for @ForeCyan()@CapName(@Word($1,1))}} {/showme {@AnsiBold()@ForeYellow()SetPet @ForeRed()Player name is invalid}}} {Petwars}
/alias {showstats %0} {/if {@InList(petwars1,@CapName($0))==1} {/showme {$0's stats: @Chr(10)@AnsiBold()@ForeCyan()@GetArray(petwars,@Var(x@CapName($0)),1)@Chr(10)@ForeGreen()Level @ForeCyan()@GetArray(petwars,@Var(x@CapName($0)),2) @ForeGreen()Class@ForeBlue():@ForeCyan()@Var(class@GetArray(petwars,@Var(x@CapName($0)),3)) @ForeGreen()Weapon@ForeBlue():@ForeCyan()@Var(weap@GetArray(petwars,@Var(x@CapName($0)),4))@Chr(10)@ForeYellow()Exp Pts Hp    Mana  AC@Chr(10)@AnsiBold()@ForeBlue()@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196) @Chr(10)@AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@CapName($0)),15), ,@Math(3-@Len(@GetArray(petwars,@Var(x@CapName($0)),15)))) @PadRight(@GetArray(petwars,@Var(x@CapName($0)),16), ,@Math(3-@Len(@GetArray(petwars,@Var(x@CapName($0)),16)))) @PadRight(@GetArray(petwars,@Var(x@CapName($0)),5), ,@Math(5-@Len(@GetArray(petwars,@Var(x@CapName($0)),5)))) @PadRight(@GetArray(petwars,@Var(x@CapName($0)),6), ,@Math(5-@Len(@GetArray(petwars,@Var(x@CapName($0)),6)))) @PadRight(@GetArray(petwars,@Var(x@CapName($0)),7), ,@Math(4-@Len(@GetArray(petwars,@Var(x@CapName($0)),7))))@Chr(10)@AnsiBold()@ForeYellow()Hr  Dr  Str Wis Int Dex Con@Chr(10)@AnsiBold()@ForeBlue()@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(196)@Chr(10)@AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@CapName($0)),8), ,@Math(3-@Len(@GetArray(petwars,@Var(x@CapName($0)),8)))) @AnsiBold()@ForeCyan()@PadRight(@GetArray(petwars,@Var(x@CapName($0)),9), ,@Math(3-@Len(@GetArray(petwars,@Var(x@CapName($0)),9)))) @GetArray(petwars,@Var(x@CapName($0)),10)  @GetArray(petwars,@Var(x@CapName($0)),11)  @GetArray(petwars,@Var(x@CapName($0)),12)  @ForeCyan()@GetArray(petwars,@Var(x@CapName($0)),13)  @ForeCyan()@GetArray(petwars,@Var(x@CapName($0)),14)@Chr(10)@ForeRed()Your current challenge status is@ForeBlue(): @ForeWhite()@Var(chal@GetArray(petwars,@Var(x@CapName($0)),20))}} {/showme {@AnsiBold()@ForeRed()That player does not have a pet}} {Petwars}} {}
/alias {save} {/loop {1,@GetCount(petwars1)} {/assign {petwars,$LoopCount,20} {0}};/write petwarssave@Time()} {Petwars}
/alias {help} {/showme {@AnsiBold()@ForeRed()Current commands:@Chr(10)createpet}} {Petwars}


/alias {showarray %0} {/if {@WordCount($0)<=1 || @WordCount($0)>3} {/showme {You supplied too many or too few perameters. "showarray Name Row Columns" (Columns are optional)}} {/if {@WordCount($0)==2} {/var saName @Word($0,1);/var saRow @Word($0,2);showarray2} {/if {@WordCount($0)==3} {/var saName @Word($0,1);/var saRow @Word($0,2);/var saCol @Word($0,3);showarray3} {/showme {Something's odd, this shouldn't print!}}}}} {ShowArray2}
/alias {showarray2} {/if {@IsNumber($saRow)==0} {/showme {@AnsiBold()@ForeRed()You supplied a non-numeric value for Rows: "@ForeYellow()$saRow@ForeRed()" -- try again!}} {/if {$saRow<0} {/showme {@AnsiBold()@ForeWhite()ShowArray: @ForeGreen()$saName @AnsiReset()};/showme {@AnsiBold()@ForeBlue()[@ForeCyan()@Abs($saRow)@ForeBlue()]@AnsiReset() @GetArray($saName,@Abs($saRow),1)}} {/showme {@AnsiBold()@ForeWhite()ShowArray: @ForeGreen()$saName @AnsiReset()};/loop {1,$saRow} {/showme {@AnsiBold()@ForeBlue()[@ForeCyan()$LoopCount@ForeBlue()]@AnsiReset() @GetArray($saName,$LoopCount,1)}}}}} {ShowArray2}
/alias {showarray3} {/if {@IsNumber($saRow)==0 || @IsNumber($saCol)==0} {/showme {@AnsiBold()@ForeRed()You supplied a non-numeric value for Row: "@ForeYellow()$saRow@ForeRed()" and/or Column: "@ForeYellow()$saCol@ForeRed()" -- try again!}} {/showme {@AnsiBold()@ForeWhite()ShowArray: @ForeGreen()$saName @AnsiReset()};/loop {1,$saRow,LoopOne} {/showme {@PadLeft(-,-,78)};/loop {1,$saCol,LoopTwo} {/showme {@AnsiBold()@ForeBlue()[@ForeCyan()$LoopOne@ForeBlue(),@ForeCyan()$LoopTwo@ForeBlue()]@AnsiReset() @GetArray($saName,$LoopOne,$LoopTwo)}}}}} {ShowArray2}
/alias {showhps} {/showme {@AnsiBold()@ForeYellow()Pet1 hp @ForeBlue()[@ForeCyan()@Var(pet1hp)@ForeBlue()] @ForeYellow()Pet2 hp @ForeBlue()[@ForeCyan()@Var(pet2hp)@ForeBlue()]} {}} {}

/alias {special0} {/if {@Random(10)>8} {/if {@Var(pet@Var(x1)hp)>@Var(pet@Var(x2)hp)} {/var {petbattle@Var(petbattle)mess} {@ConCat(@Var(petbattle@Var(petbattle)mess),@Chr(10)@AnsiBold()@ForeYellow()@GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) appears to be winning the battle!)}} {/var {petbattle@Var(petbattle)mess} {@ConCat(@Var(petbattle@Var(petbattle)mess),@Chr(10)@AnsiBold()@ForeYellow()@GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) weakens under the assault...)}}} {/if {@Random(10)>9} {/var {petbattle@Var(petbattle)mess} {@ConCat(@Var(petbattle@Var(petbattle)mess),@Chr(10)@AnsiBold()@ForeRed()@GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) snarls at @Var(pet@Var(x2))'s pet\, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1).)}} {}}} {Petwars}

/alias {special1} {hasweapon @Var(pet@Var(x1));/if {@Var(x)} {warweapon} {warnoweapon}} {Petwars}

/alias {skill %0} {/if {@Math(@Random(@Word($0,3))+@Random(@GetArray(petprof,@Word($0,1),@Var(@Word($0,2))) > @Word($0,4)} {/var {x} {1}} {/var {x} {0}}} {Petwars}

/alias {warweapon} {/if {@GetArray(petwars,@Var(x@Var(pet@Var(x2))),3)>3} {bash} {slash}} {Petwars}

/alias {bash} {skill @Var(x@Var(pet@Var(x1))) bash 100 50;bash$x} {Petwars}
/alias {bash1} {battlemess @AnsiReset()@ForeWhite()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) sends @Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1) to the ground with a powerful bash.} {Petwars}
/alias {bash0} {battlemess @AnsiReset()@ForeWhite()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) attempts to bash @Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1) and hits a glancing blow.} {Petwars}


/alias {slash} {battlemess @AnsiBold()@ForeYellow()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) lashes out at @Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1) with its weapon.;petattack @Random(@Math(184+(30*@Var(pet@Var(x1)striking)))} {Petwars}

/alias {warnoweapon} {/if {@Random(2)>1} {kickhit} {kickmiss}} {Petwars}
/alias {kickhit} {/var {dam} {@Math(@Random(@GetArray(petwars,@Var(x@Var(x1)),2))+@Random(@GetArray(petwars,@Var(x@Var(x1)),2)))};/if {@Var(dam)>@Var(pet@Var(x2)hp)} {petkill @Chr(10)@AnsiReset()@ForeWhite()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) finishes @Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1) with a powerful kick!} {/var {petbattle@Var(petbattle)mess} {@ConCat(@Var(petbattle@Var(petbattle)mess),@Chr(10)@AnsiReset()@ForeWhite()@Var(pet@Var(x1))'s pet\, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) lands a kick on @Var(pet@Var(x2))'s pet\, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1).)}} {Petwars}
/alias {kickmiss} {battlemess @AnsiReset()@ForeWhite()@Var(pet@Var(x1))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x1))),1) misses a kick on @Var(pet@Var(x2))'s pet, @GetArray(petwars,@Var(x@Var(pet@Var(x2))),1).}} {Petwars}


/var rage 1 Petwars
/var kick 2 Petwars
/var bash 3 Petwars
/var slice 4 Petwars
/var trip 5 Petwars
/var backstab 6 Petwars
/var {minor heal} 7 Petwars
/var heal 8 Petwars
/var {greater heal} 9 Petwars
/var {lesser harm} 10 Petwars
/var harm 11 Petwars
/var {greater harm} 12 Petwars
/var {ice arrow} 13 Petwars
/var {frost shards} 14 Petwars
/var blizzard 15 Petwars
/var curse 16 Petwars

/var skill1 rage Petwars
/var skill2 kick Petwars
/var skill3 bash Petwars
/var skill4 slice Petwars
/var skill5 trip Petwars
/var skill6 backstab Petwars
/var skill7 {minor heal} Petwars
/var skill8 heal Petwars
/var skill9 {greater heal} Petwars
/var skill10 {lesser harm} Petwars
/var skill11 harm Petwars
/var skill12 {greater harm} Petwars
/var skill13 {ice arrow} Petwars
/var skill14 {frost shards} Petwars
/var skill15 blizzard Petwars
/var skill16 curse Petwars



/var {combatdebug} {1} {Petwars}
/variable {acarr} {7} {Petwars}
/variable {acbon} {-3} {Petwars}
/variable {acbon1} {8} {Petwars}
/variable {acbon2} {20} {Petwars}
/variable {acmax} {-103} {Petwars}
/variable {addac} {-4} {Petwars}
/variable {addcon} {1} {Petwars}
/variable {adddex} {1} {Petwars}
/variable {adddr} {1} {Petwars}
/variable {addhp} {5} {Petwars}
/variable {addhr} {1} {Petwars}
/variable {addint} {1} {Petwars}
/variable {addmana} {5} {Petwars}
/variable {addstr} {1} {Petwars}
/variable {addweapon} {1} {Petwars}
/variable {addwis} {1} {Petwars}
/variable {battle} {0} {Petwars}
/variable {battlemess} {[1m[32mSolinor's pet, die.bitch's pierce [36mmassacres [32mHoju's pet, It!} {}
/variable {bsdam} {16} {Petwars}
/variable {ch1temp} {Hezukeh[out]} {Petwars}
/variable {ch2temp} {Hezukeh} {Petwars}
/variable {chal0} {none} {Petwars}
/variable {chal1} {challenging} {Petwars}
/variable {chal2} {being challenged} {Petwars}
/variable {chal3} {battling} {Petwars}
/variable {classarr} {3} {Petwars}
/variable {class0} {none} {Petwars}
/variable {class1} {warrior} {Petwars}
/variable {class2} {thief} {Petwars}
/variable {class3} {cleric} {Petwars}
/variable {class4} {mage} {Petwars}
/variable {classwarrior} {1} {Petwars}
/variable {classthief} {2} {Petwars}
/variable {classcleric} {3} {Petwars}
/variable {classmage} {4} {Petwars}
/variable {classarrwarrior} {24} {Petwars}
/variable {classarrthief} {25} {Petwars}
/variable {classarrcleric} {26} {Petwars}
/variable {classarrmage} {27} {Petwars}
/variable {clhit0} {6} {Petwars}
/variable {clhit1} {8} {Petwars}
/variable {clhit2} {7} {Petwars}
/variable {clhit3} {5} {Petwars}
/variable {clhit4} {4} {Petwars}

/variable {con10} {1} {Petwars}
/variable {con11} {2} {Petwars}
/variable {con12} {5} {Petwars}
/variable {con13} {7} {Petwars}
/variable {con14} {10} {Petwars}
/variable {con15} {12} {Petwars}
/variable {con16} {15} {Petwars}
/variable {con17} {17} {Petwars}
/variable {con18} {20} {Petwars}
/variable {conarr} {14} {Petwars}
/variable {conmax} {19} {Petwars}

/array {damage} {131} {Petwars}
/assign {damage} {1} {barely touches} {Petwars}
/assign {damage} {10} {draws blood from} {Petwars}
/assign {damage} {100} {annihilates} {Petwars}
/assign {damage} {101} {horribly maims} {Petwars}
/assign {damage} {102} {horribly maims} {Petwars}
/assign {damage} {103} {horribly maims} {Petwars}
/assign {damage} {104} {horribly maims} {Petwars}
/assign {damage} {105} {horribly maims} {Petwars}
/assign {damage} {106} {horribly maims} {Petwars}
/assign {damage} {107} {horribly maims} {Petwars}
/assign {damage} {108} {horribly maims} {Petwars}
/assign {damage} {109} {horribly maims} {Petwars}
/assign {damage} {11} {draws blood from} {Petwars}
/assign {damage} {110} {horribly maims} {Petwars}
/assign {damage} {111} {horribly maims} {Petwars}
/assign {damage} {112} {horribly maims} {Petwars}
/assign {damage} {113} {horribly maims} {Petwars}
/assign {damage} {114} {horribly maims} {Petwars}
/assign {damage} {115} {horribly maims} {Petwars}
/assign {damage} {116} {horribly maims} {Petwars}
/assign {damage} {117} {horribly maims} {Petwars}
/assign {damage} {118} {horribly maims} {Petwars}
/assign {damage} {119} {horribly maims} {Petwars}
/assign {damage} {12} {smites} {Petwars}
/assign {damage} {120} {horribly maims} {Petwars}
/assign {damage} {121} {horribly maims} {Petwars}
/assign {damage} {122} {horribly maims} {Petwars}
/assign {damage} {123} {horribly maims} {Petwars}
/assign {damage} {124} {horribly maims} {Petwars}
/assign {damage} {125} {horribly maims} {Petwars}
/assign {damage} {126} {horribly maims} {Petwars}
/assign {damage} {127} {horribly maims} {Petwars}
/assign {damage} {128} {horribly maims} {Petwars}
/assign {damage} {129} {horribly maims} {Petwars}
/assign {damage} {13} {smites} {Petwars}
/assign {damage} {130} {horribly maims} {Petwars}
/assign {damage} {131} {visciously rends} {Petwars}
/assign {damage} {14} {smites} {Petwars}
/assign {damage} {15} {massacres} {Petwars}
/assign {damage} {16} {massacres} {Petwars}
/assign {damage} {17} {massacres} {Petwars}
/assign {damage} {18} {massacres} {Petwars}
/assign {damage} {19} {massacres} {Petwars}
/assign {damage} {2} {barely touches} {Petwars}
/assign {damage} {20} {massacres} {Petwars}
/assign {damage} {21} {decimates} {Petwars}
/assign {damage} {22} {decimates} {Petwars}
/assign {damage} {23} {decimates} {Petwars}
/assign {damage} {24} {decimates} {Petwars}
/assign {damage} {25} {decimates} {Petwars}
/assign {damage} {26} {devastates} {Petwars}
/assign {damage} {27} {devastates} {Petwars}
/assign {damage} {28} {devastates} {Petwars}
/assign {damage} {29} {devastates} {Petwars}
/assign {damage} {3} {scratches} {Petwars}
/assign {damage} {30} {devastates} {Petwars}
/assign {damage} {31} {maims} {Petwars}
/assign {damage} {32} {maims} {Petwars}
/assign {damage} {33} {maims} {Petwars}
/assign {damage} {34} {maims} {Petwars}
/assign {damage} {35} {maims} {Petwars}
/assign {damage} {36} {maims} {Petwars}
/assign {damage} {37} {maims} {Petwars}
/assign {damage} {38} {maims} {Petwars}
/assign {damage} {39} {maims} {Petwars}
/assign {damage} {4} {bruises} {Petwars}
/assign {damage} {40} {maims} {Petwars}
/assign {damage} {41} {mutilates} {Petwars}
/assign {damage} {42} {mutilates} {Petwars}
/assign {damage} {43} {mutilates} {Petwars}
/assign {damage} {44} {mutilates} {Petwars}
/assign {damage} {45} {mutilates} {Petwars}
/assign {damage} {46} {mutilates} {Petwars}
/assign {damage} {47} {mutilates} {Petwars}
/assign {damage} {48} {mutilates} {Petwars}
/assign {damage} {49} {mutilates} {Petwars}
/assign {damage} {5} {hits} {Petwars}
/assign {damage} {50} {mutilates} {Petwars}
/assign {damage} {51} {pulverizes} {Petwars}
/assign {damage} {52} {pulverizes} {Petwars}
/assign {damage} {53} {pulverizes} {Petwars}
/assign {damage} {54} {pulverizes} {Petwars}
/assign {damage} {55} {pulverizes} {Petwars}
/assign {damage} {56} {pulverizes} {Petwars}
/assign {damage} {57} {pulverizes} {Petwars}
/assign {damage} {58} {pulverizes} {Petwars}
/assign {damage} {59} {pulverizes} {Petwars}
/assign {damage} {6} {injures} {Petwars}
/assign {damage} {60} {pulverizes} {Petwars}
/assign {damage} {61} {demolishes} {Petwars}
/assign {damage} {62} {demolishes} {Petwars}
/assign {damage} {63} {demolishes} {Petwars}
/assign {damage} {64} {demolishes} {Petwars}
/assign {damage} {65} {demolishes} {Petwars}
/assign {damage} {66} {demolishes} {Petwars}
/assign {damage} {67} {demolishes} {Petwars}
/assign {damage} {68} {demolishes} {Petwars}
/assign {damage} {69} {demolishes} {Petwars}
/assign {damage} {7} {injures} {Petwars}
/assign {damage} {70} {demolishes} {Petwars}
/assign {damage} {71} {mangles} {Petwars}
/assign {damage} {72} {mangles} {Petwars}
/assign {damage} {73} {mangles} {Petwars}
/assign {damage} {74} {mangles} {Petwars}
/assign {damage} {75} {mangles} {Petwars}
/assign {damage} {76} {mangles} {Petwars}
/assign {damage} {77} {mangles} {Petwars}
/assign {damage} {78} {mangles} {Petwars}
/assign {damage} {79} {mangles} {Petwars}
/assign {damage} {8} {wounds} {Petwars}
/assign {damage} {80} {mangles} {Petwars}
/assign {damage} {81} {obliterates} {Petwars}
/assign {damage} {82} {obliterates} {Petwars}
/assign {damage} {83} {obliterates} {Petwars}
/assign {damage} {84} {obliterates} {Petwars}
/assign {damage} {85} {obliterates} {Petwars}
/assign {damage} {86} {obliterates} {Petwars}
/assign {damage} {87} {obliterates} {Petwars}
/assign {damage} {88} {obliterates} {Petwars}
/assign {damage} {89} {obliterates} {Petwars}
/assign {damage} {9} {wounds} {Petwars}
/assign {damage} {90} {obliterates} {Petwars}
/assign {damage} {91} {obliterates} {Petwars}
/assign {damage} {92} {annihilates} {Petwars}
/assign {damage} {93} {annihilates} {Petwars}
/assign {damage} {94} {annihilates} {Petwars}
/assign {damage} {95} {annihilates} {Petwars}
/assign {damage} {96} {annihilates} {Petwars}
/assign {damage} {97} {annihilates} {Petwars}
/assign {damage} {98} {annihilates} {Petwars}
/assign {damage} {99} {annihilates} {Petwars}
/variable {dex10} {0} {Petwars}
/variable {dex11} {1} {Petwars}
/variable {dex12} {2} {Petwars}
/variable {dex13} {2} {Petwars}
/variable {dex14} {3} {Petwars}
/variable {dex15} {3} {Petwars}
/variable {dex16} {4} {Petwars}
/variable {dex17} {4} {Petwars}
/variable {dex18} {5} {Petwars}
/variable {dexarr} {13} {Petwars}
/variable {dexmax} {19} {Petwars}
/variable {drarr} {9} {Petwars}
/variable {drbon1} {6} {Petwars}
/variable {drbon2} {4} {Petwars}
/variable {drgain1} {4} {Petwars}
/variable {drgain2} {0} {Petwars}
/variable {drmax} {101} {Petwars}
/variable {hparr} {5} {Petwars}
/variable {hpgain1} {8} {Petwars}
/variable {hpgain2} {0} {Petwars}
/variable {hpmax} {10005} {Petwars}
/variable {hrarr} {8} {Petwars}
/variable {hrgain1} {4} {Petwars}
/variable {hrgain2} {0} {Petwars}
/variable {hrmax} {101} {Petwars}
/variable {int10} {0} {Petwars}
/variable {int11} {3} {Petwars}
/variable {int12} {9} {Petwars}
/variable {int13} {12} {Petwars}
/variable {int14} {18} {Petwars}
/variable {int15} {21} {Petwars}
/variable {int16} {27} {Petwars}
/variable {int17} {30} {Petwars}
/variable {int18} {36} {Petwars}
/variable {intarr} {12} {Petwars}
/variable {intmax} {19} {Petwars}
/variable {levelarr} {2} {Petwars}
/variable {manaarr} {6} {Petwars}
/variable {managain1} {0} {Petwars}
/variable {managain2} {0} {Petwars}
/variable {manamax} {5005} {Petwars}
/variable {messages} {[1m[31m## [36mPoster                     Message} {}
/variable {numbattle} {0} {Petwars}
/variable {numbattles} {4216} {Petwars}
/variable {pet1} {Solinor} {Petwars}
/variable {pet1cond} {is in excellent condition.} {Petwars}
/variable {pet1condx} {100} {Petwars}
/variable {pet1dam} {14} {Petwars}
/variable {pet1damtemp} {massacres} {Petwars}
/variable {pet1hp} {48} {Petwars}
/variable {pet1mana} {25} {Petwars}
/variable {pet1mess} {-} {Petwars}
/variable {pet1sanc} {0} {}
/variable {pet1spec} {0} {Petwars}
/variable {pet1specmess} {-} {Petwars}
/variable {pet1striking} {0} {Petwars}
/variable {pet1weapon} {'s pierce} {Petwars}
/variable {pet1weapondam} {8} {Petwars}
/variable {pet1} {-} {Petwars}
/variabl {pet2} {-} {Petwars}
/variabl {pet3} {-} {Petwars}
/variabl {pet4} {-} {Petwars}

/variable {pet2cond} {is dead.} {Petwars}
/variable {pet2condx} {0} {Petwars}
/variable {pet2dam} {10} {Petwars}
/variable {pet2damtemp} {draws blood from} {Petwars}
/variable {pet2hp} {10} {Petwars}
/variable {pet2mana} {25} {Petwars}
/variable {pet2mess} {[1m[32mHoju's pet, It [36mdraws blood from [32mSolinor's pet, die.bitch!} {Petwars}
/variable {pet2sanc} {0} {}
/variable {pet2spec} {0} {Petwars}
/variable {pet2specmess} {[0m[37mHed's pet, BlueDuck cunningly lodges a knife into Xaxersic's pet, MightKnowKungFU.} {}
/variable {pet2striking} {0} {}
/empty {pet2weapon} {Petwars}
/variable {pet2weapondam} {6} {Petwars}
/variable {prompt0} {off} {Petwars}
/variable {prompt1} {on} {Petwars}
/variable {ptgain1} {0} {Petwars}
/variable {ptgain2} {0} {Petwars}
/variable {qnum} {4216} {Petwars}
/variable {queue} {[1m[31m## [36mPlayers} {}
/variable {rcon10} {2} {Petwars}
/variable {rcon11} {4} {Petwars}
/variable {rcon12} {10} {Petwars}
/variable {rcon13} {14} {Petwars}
/variable {rcon14} {20} {Petwars}
/variable {rcon15} {24} {Petwars}
/variable {rcon16} {30} {Petwars}
/variable {rcon17} {36} {Petwars}
/variable {rcon18} {40} {Petwars}
/variable {saCol} {null} {ShowArray}
/variable {saName} {null} {ShowArray}
/variable {saRow} {null} {ShowArray}
/variable {spelldam} {61} {Petwars}
/variable {spellsanc} {8} {Petwars}
/variable {spellsancarr} {22} {Petwars}
/variable {spellstriking} {6} {Petwars}
/variable {spellstrikingarr} {23} {Petwars}
/variable {stcoac} {3} {Petwars}
/variable {stcocon} {6} {Petwars}
/variable {stcodex} {6} {Petwars}
/variable {stcodr} {6} {Petwars}
/variable {stcohp} {6} {Petwars}
/variable {stcohr} {4} {Petwars}
/variable {stcoint} {6} {Petwars}
/variable {stcomana} {4} {Petwars}
/variable {stcostr} {6} {Petwars}
/variable {stcoweapon} {60} {Petwars}
/variable {stcowis} {6} {Petwars}
/variable {str10} {0} {Petwars}
/variable {str11} {1} {Petwars}
/variable {str12} {1} {Petwars}
/variable {str13} {2} {Petwars}
/variable {str14} {2} {Petwars}
/variable {str15} {2} {Petwars}
/variable {str16} {3} {Petwars}
/variable {str17} {3} {Petwars}
/variable {str18} {4} {Petwars}
/variable {strarr} {10} {Petwars}
/variable {strmax} {19} {Petwars}
/variable {tempmana} {24} {}
/variable {weap1} {none} {Petwars}
/variable {weap1dam} {4 2} {Petwars}
/variable {weap2} {bronze} {Petwars}
/variable {weap2dam} {4 5} {Petwars}
/variable {weap3} {iron} {Petwars}
/variable {weap3dam} {8 4} {Petwars}
/variable {weap4} {steel} {Petwars}
/variable {weap4dam} {8 6} {Petwars}
/variable {weap5} {silver} {Petwars}
/variable {weap5dam} {8 8} {Petwars}
/variable {weap6} {gold} {Petwars}
/variable {weap6dam} {10 8} {Petwars}
/variable {weap7} {platinum} {Petwars}
/variable {weap7dam} {10 10} {Petwars}
/variable {weapnone} {none} {Petwars}
/variable {weapnonedam} {4 2} {Petwars}
/variable {weaponarr} {4} {Petwars}
/variable {weaponmax} {8} {Petwars}
/variable {whoconnect} {Kirius} {Petwars}
/variable {whoison} {} {Petwars}
/variable {winpts1} {5} {Petwars}
/variable {winpts2} {5} {Petwars}
/variable {wis10} {1} {Petwars}
/variable {wis11} {2} {Petwars}
/variable {wis12} {3} {Petwars}
/variable {wis13} {4} {Petwars}
/variable {wis14} {5} {Petwars}
/variable {wis15} {6} {Petwars}
/variable {wis16} {7} {Petwars}
/variable {wis17} {8} {Petwars}
/variable {wis18} {9} {Petwars}
/variable {wisarr} {11} {Petwars}
/variable {wismax} {19} {Petwars}

/gag {# %0 is now allowed to snoop} {}
/listadd {class} {Petwars}
/itemadd {class} {3}
/itemadd {class} {4}
/itemadd {class} {2}
/itemadd {class} {1}
/listadd {cleric} {Petwars}
/itemadd {cleric} {harm}
/itemadd {cleric} {heal}
/listadd {kickmess} {Petwars}
/itemadd {kickmess} {gracefully}
/itemadd {kickmess} {powerfully}
/itemadd {kickmess} {tactfully}
/listadd {mage} {Petwars}
/itemadd {mage} {mm}
/itemadd {mage} {weaken}
/listadd {messages} {Petwars}
/itemadd {messages} {[1m[36mDagz[34m: [32mkhaoric gives mighty hand jobs! i recommend the rusty trombones as well.}
/listadd {petwars1} {Petwars}
/listadd {petwars2} {Petwars}
/listadd {player} {Petwars}
/listadd {queue} {Petwars}
/listadd {spells} {Petwars}
/itemadd {spells} {sanc}
/itemadd {spells} {striking}
/listadd {stco} {Petwars}
/itemadd {stco} {ac}
/itemadd {stco} {class}
/itemadd {stco} {con}
/itemadd {stco} {dex}
/itemadd {stco} {dr}
/itemadd {stco} {hp}
/itemadd {stco} {hr}
/itemadd {stco} {int}
/itemadd {stco} {level}
/itemadd {stco} {mana}
/itemadd {stco} {str}
/itemadd {stco} {weapon}
/itemadd {stco} {wis}
/listadd {thief} {Petwars}
/itemadd {thief} {throw}
/listadd {throwmess} {Petwars}
/itemadd {throwmess} {cunningly}
/itemadd {throwmess} {quickly}
/itemadd {throwmess} {skillfully}
/itemadd {throwmess} {swiftfully}
/listadd {warrior} {Petwars}
/itemadd {warrior} {kick}
/loadlibrary {FileLog.dll}
/array {health} {100} {Petwars}
/assign {health} {1} {barely clings to life.}
/assign {health} {2} {barely clings to life.}
/assign {health} {3} {barely clings to life.}
/assign {health} {4} {barely clings to life.}
/assign {health} {5} {barely clings to life.}
/assign {health} {6} {barely clings to life.}
/assign {health} {7} {barely clings to life.}
/assign {health} {8} {pales visibly as death nears.}
/assign {health} {9} {pales visibly as death nears.}
/assign {health} {10} {pales visibly as death nears.}
/assign {health} {11} {pales visibly as death nears.}
/assign {health} {12} {pales visibly as death nears.}
/assign {health} {13} {pales visibly as death nears.}
/assign {health} {14} {pales visibly as death nears.}
/assign {health} {15} {is vomiting blood.}
/assign {health} {16} {is vomiting blood.}
/assign {health} {17} {is vomiting blood.}
/assign {health} {18} {is vomiting blood.}
/assign {health} {19} {is vomiting blood.}
/assign {health} {20} {is vomiting blood.}
/assign {health} {21} {is vomiting blood.}
/assign {health} {22} {has many grievous wounds.}
/assign {health} {23} {has many grievous wounds.}
/assign {health} {24} {has many grievous wounds.}
/assign {health} {25} {has many grievous wounds.}
/assign {health} {26} {has many grievous wounds.}
/assign {health} {27} {has many grievous wounds.}
/assign {health} {28} {has many grievous wounds.}
/assign {health} {29} {looks pretty awful.}
/assign {health} {30} {looks pretty awful.}
/assign {health} {31} {looks pretty awful.}
/assign {health} {32} {looks pretty awful.}
/assign {health} {33} {looks pretty awful.}
/assign {health} {34} {looks pretty awful.}
/assign {health} {35} {looks pretty awful.}
/assign {health} {36} {has some large, gaping wounds.}
/assign {health} {37} {has some large, gaping wounds.}
/assign {health} {38} {has some large, gaping wounds.}
/assign {health} {39} {has some large, gaping wounds.}
/assign {health} {40} {has some large, gaping wounds.}
/assign {health} {41} {has nasty wounds and bleeding cuts.}
/assign {health} {42} {has nasty wounds and bleeding cuts.}
/assign {health} {43} {has nasty wounds and bleeding cuts.}
/assign {health} {44} {has nasty wounds and bleeding cuts.}
/assign {health} {45} {has nasty wounds and bleeding cuts.}
/assign {health} {46} {has nasty wounds and bleeding cuts.}
/assign {health} {47} {has nasty wounds and bleeding cuts.}
/assign {health} {48} {grimaces with pain.}
/assign {health} {49} {grimaces with pain.}
/assign {health} {50} {grimaces with pain.}
/assign {health} {51} {grimaces with pain.}
/assign {health} {52} {grimaces with pain.}
/assign {health} {53} {grimaces with pain.}
/assign {health} {54} {grimaces with pain.}
/assign {health} {55} {has quite a few wounds.}
/assign {health} {56} {has quite a few wounds.}
/assign {health} {57} {has quite a few wounds.}
/assign {health} {58} {has quite a few wounds.}
/assign {health} {59} {has quite a few wounds.}
/assign {health} {60} {has quite a few wounds.}
/assign {health} {61} {has quite a few wounds.}
/assign {health} {62} {winces in pain.}
/assign {health} {63} {winces in pain.}
/assign {health} {64} {winces in pain.}
/assign {health} {65} {winces in pain.}
/assign {health} {66} {winces in pain.}
/assign {health} {67} {winces in pain.}
/assign {health} {68} {winces in pain.}
/assign {health} {69} {has some minor wounds.}
/assign {health} {70} {has some minor wounds.}
/assign {health} {71} {has some minor wounds.}
/assign {health} {72} {has some minor wounds.}
/assign {health} {73} {has some minor wounds.}
/assign {health} {74} {has some minor wounds.}
/assign {health} {75} {has some minor wounds.}
/assign {health} {76} {has some small bruises.}
/assign {health} {77} {has some small bruises.}
/assign {health} {78} {has some small bruises.}
/assign {health} {79} {has some small bruises.}
/assign {health} {80} {has some small bruises.}
/assign {health} {81} {has some small bruises.}
/assign {health} {82} {has some small bruises.}
/assign {health} {83} {has a few scratches.} 
/assign {health} {84} {has a few scratches.} 
/assign {health} {85} {has a few scratches.} 
/assign {health} {86} {has a few scratches.} 
/assign {health} {87} {has a few scratches.} 
/assign {health} {88} {has a few scratches.} 
/assign {health} {89} {has a few scratches.} 
/assign {health} {90} {is barely scratched.} 
/assign {health} {91} {is barely scratched.} 
/assign {health} {92} {is barely scratched.} 
/assign {health} {93} {is barely scratched.} 
/assign {health} {94} {is barely scratched.} 
/assign {health} {95} {is barely scratched.} 
/assign {health} {96} {is barely scratched.} 
/assign {health} {97} {is barely scratched.} 
/assign {health} {98} {is barely scratched.} 
/assign {health} {99} {is barely scratched.} 
/assign {health} {100} {is in excellent condition.}

/array {petwars} {250,50} {Petwars}
/array {petprof} {250,25} {Petwars}
/chatname {Petwars}

/unvar _