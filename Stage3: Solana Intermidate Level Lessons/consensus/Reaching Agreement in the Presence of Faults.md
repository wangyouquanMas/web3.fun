Reaching Agreement in the Presence of Faults
M. PEASE, R, SHOSTAK, AND L. LAMPORT
SRI Internatwnal, Menlo Park, California
ABSTRACT. The problem addressed here concerns a set of isolated processors, some unknown subset of which
may be faulty, that communicate only by means of two-party messages. Each nonfaulty processor has a private
value of reformation that must be communicated to each other nonfanlty processor. Nonfaulty processors always
communicate honestly, whereas faulty processors may lie The problem is to devise an algorithm in which
processors communicate their own values and relay values received from others that allows each nonfaulty
processor to refer a value for each other processor The value referred for a nonfanlty processor must be that
processor's private value, and the value inferred for a faulty one must be consistent wRh the corresponding value
inferred by each other nonfanlty processor
It is shown that the problem is solvable for, and only for, n >_ 3m + 1, where m IS the number of faulty
processors and n is the total number. It is also shown that if faulty processors can refuse to pass on reformation
but cannot falsely relay information, the problem is solvable for arbitrary n _> m _> 0. This weaker assumption
can be approxunated m practice using cryptographic methods
KEY WORDS AND eHRASES, agreement, authentication, consistency, distributed executive, fault avoidance, fault
tolerance, synchronization, voting
CR CATEGORIES: 3.81, 4.39, 5.29, 5.39, 6.22
1. Introduction
Fault-tolerant systems often require a means by which independent processors or processes
can arrive at an exact mutual agreement of some kind. It may be necessary, for example,
for the processors of a redundant system to synchronize their internal docks periodically.
Or they may have to settle upon a value of a time-varying input sensor that gives each of
them a slightly different reading. In the absence of faults reaching a satisfactory mutual
agreement is usually an easy matter. In most cases it suffices simply to exchange values
(times, in the case of clock synchronization) and compute some kind of average. In the
presence of faulty processors, however, simple exchanges cannot be relied upon; a bad
processor might report one value to a given processor and another value to some other
processors, causing each to calculate a different "average."
One might imagine that the effects of faulty processors could be dealt with through the
use of voting schemes revolving more than one round of information exchange; such
schemes might force faulty processors to reveal themselves as faulty or at least to behave
consistently enough with respect to the nonfaulty processors to allow the latter to reach an exact agreement. As we will show, it is not always possible to devise schemes of this kind,
even if it is known that the faulty processors are in a minority. Algorithms that allow exact
agreement to be reached by the nonfaulty processors do exist, however, if they sufficiently
outnumber the faulty ones.
Our results are formulated using the notion of interactive consistency, which we define m are faulty. It is not known, however, which processors are faulty. Suppose that the
processors can commumcate only by means of two-party messages. The communication
medium is presumed to be fail-safe and of negligible delay. The sender of a message,
moreover, Is always identifiable by the receiver. Suppose also that each processor p has
some private value of information Vp (such as its clock value or its reading of some sensor).
The question is whether for given m, n _> 0, it is possible to devise an algorithm based on
an exchange of messages that will allow each nonfaulty processor/) to compute a vector of
values with an element for each of the n processors, such that
(1) the nonfaulty processors compute exactly the same vector;
(2) the element of this vector corresponding to a given nonfaulty processor is the private
value of that processor.
Note that the algorithm need not reveal which processors are faulty, and that the
elements of the computed vector corresponding to faulty processors may be arbitrary; it
matters only that the nonfaulty processors compute exactly the same value for any given
faulty processor.
We say that s nfaulty processors to come to a consistent view of the values held by all the processors,
including the faulty ones. The computed vector is called an interactive consistency (i.c.)
vector. Once mteractwe consistency has been achieved, each nonfaulty processor can apply
an averaging or filtering function to the i.c. vector, according to the needs of the application.
Since each nonfaulty processor applies this function to the same vector of values, an exact
agreement is necessarily reached.
We show in the following sections that algorithms can be devised to guarantee interactive
consistency for and only for n, m such that n >_ 3m + 1. It will follow, in particular, that
a minimum of four processors is required in the single-fault case. We also show, however,
that interactive consistency can be assured for arbitrary n _> m _> 0 if it is assumed that
faulty processors can refuse to pass on information obtained from other processors but
cannot falsely report this information. This assumption can be approximated in practice
using authenticators, which we discuss in Section 5.
We begin in Section 2 with a description of the single-fault case. Section 3 is concerned
with the generalization to n _> 3m + 1 and Section 4 with an impossibility argument for n
_< 3m. Section 5 gives an algorithm for arbitrary n _> m _> 0 that works under the restricted
assumption stated above. Conclusions and issues for future study are given in Section 6.
Problems similar to the one considered here have been studied by Davies and
Wakerly [1].
2. The Single-F In order to give the reader a feeling for the problem, we begin with a procedure for
obtaining interactwe consistency in the simple case ofm = 1, n = 4. The procedure consists
of an exchange of messages, followed by the computation of the interactive consistency
vector on the basis of the results of the exchange.
Two rounds of reformation exchange are required. In the first round the processors
exchange their private values. In the second round they exchange the results obtained in
the first round. The faulty processor 0f there is one) may "lie," of course, or refuse to send
messages. If a nonfaulty processor p fails to receive a message it expects from some other
processor, p simply chooses a value at random and acts as if that value had been sent.
The exchange having been completed, each nonfaulty processor p records its private
value Vp for the element of the interactive consistency corresponding to p itself. The
element corresponding to every other processor q is obtained by examining the three
received reports of q's value (one of these was obtained directly from q in the first round,
and the others from the remaining two processors in the second round). If at least two of 
230 M. PEASE, R. SHOSTAK, AND L. LAMPORT
the three reports agree, the majority value is used. Otherwise, a default value such as
"NIL" is used.
To see that this procedure assures interactive consistency, first note that if q is nonfaulty,
p will receive Vq both from q and from the other nonfaulty processor(s). Thusp will record
Vq for q as desired. Now suppose q is faulty. We must show only that p and the other two
nonfaulty processors record the same value for q. If every nonfaulty processor records
NIL, we are done. Otherwise, some nonfaulty processor, say p, records a non-NIL value
v, having received v from at least two other processors. Now ifp received v from both of
the other nonfaulty processors, each other nonfaulty processor must receive v from every
processor other than p (and possibly from p as well); every nonfaulty processor will thus
record v. Otherwise, p must have received v from all processors other than some other
nonfaulty processor p'. In this case p' received v from all processors other than q (so p'
records v), and all other nonfaulty processors received v from all processors other than p'.
All nonfaulty processors therefore record v as required. 
3. A Procedure for n >_ 3m + 1
Recall that the procedure given in the last section requires two rounds of information
exchange, the first consisting of communications of the form "my private value is" and
the second consisting of communications of the form "processor x told me his private
value is .... " In the general case of m faults, m + 1 rounds are required. In order to
describe the algorithm, it will be convenient to characterize this exchange of messages in
a more formal way.
Let P be the set of processors and V a set of values. For k >_ 1, we define a k-level
scenario as a mapping from the set of nonempty strings (possibly having repetitions) over
P of length _<k + 1, to V. For a given k-level scenario o and string w -~ pip2 • • • pr, 2 _<
r _< k + l, o(w) is interpreted as the value p2 tells pl that p3 told p2 that p4 told p3 ... that
p, told p,-~ is pr'S private value. For a single-element string p, o(p) simply designates p's
private value V r. A k-level scenario thus summarizes the outcome of a k-round exchange
of information. (Note that if a faulty processor lies about who gave it information, this is
equivalent to lying about a value it was given.) Note also that for a given subset of
nonfaulty processors, only certain mappings are possible scenarios; in particular, since
nonfaulty processors are always truthful in relaying information, a scenario must satisfy
o(pqw) = o(qw)
for each nonfaulty processor q, arbitrary processor p, and string w.
The messages a processor p receives in a scenario o are given by the restriction op of o
to strings beginning with p. The procedure we present now for arbitrary m >_ 0, n >_
3m + 1, is described in terms of p's computation, for a given Op, of the element of
the interactive-consistency vector corresponding to each processor q. The computation is
as follows:
(1) If for some subset Q ofPofsize >(n + m)/2 and some value v, op(pwq) = v for each
string w over Q of length _<m, p records v.
(2) Otherwise, the algorithm for m - 1, n - 1 is recursively applied with P replaced by
P - {q}, and op by the mapping Op defmed by
~,,(pw) ffi op(pwq)
for each string w of length _<m over P - {q}. If at least [(n + m)/2J of the n - 1 elements
in the vector obtained in the recursiv¢ call agree, p records the common value, otherwise
p records NIL. Note that 69 corresponds to the m-level subscenario of o in which q is excluded and
in which each processor's private value is the value it obtains directly from q m o. Note
also that the algorithm essentially reduces to the one given in the last section in the case
m ffi l, n -- 4. 
Reaching Agreement in the Presence of Faults 231
The proof that the algorithm given above does indeed assure interactive consistency
proceeds by reduction on m:
Basis m = O. In this case no processor is faulty, and the algorithm always terminates
m step (1) withp recording Vq for q.
Induction Step m > 0. First note that if q is nonfaulty, op(pwq) = Vq for each string w
(including the empty string) of length _<m over the set of nonfaulty processors. This set has
n - m members (which, since n > 3m, is >(n + m)/2) and so satisfies the requirements for
Q in step (1) of the algorithm. Any other set satisfying these requirements, moreover, must
contain a nonfaulty processor (since it must be of size >(n + m)/2, and n _> 3m + 1) and
must therefore also yield Vq as the common value. The algorithm thus terminates at step
(1), andp records Vq and q as required.
Now suppose that q is faulty. We must show that the value p records for q agrees with
the value each other nonfaulty processor p' records for q.
First consider the case m which bothp andp' exit the procedure at step (1), each having
found an appropriate set Q. Since each such set has more than (n + m)/2 members, and
since P has only n members in all, the two sets must have more than 2((n + m)/2) - n =
m common members. Since at least one of these must be nonfaulty, the two sets must give
rise to the same value v, as required. Next suppose that p' exits at step (1), having found an appropriate set Q and common
value v, and that p executes step (2). We claim that in the vector of n - 1 elements that p
computes in the recursive call, the elements corresponding to members of Q = Q - (q} are
equal to v. Since Q has at least t(n + m)/2J members, it will then follow that p records v
in accordance with step (2). To see that the elements corresponding to members of Q are
indeed equal to v, recall that the mapping Op that p uses to compute the vector in the
recursive call is the restriction, to strings beginning with p, of the m-level scenario Jr
defined by
~(w) = o(wq)
for each string w of length _<m over P - {q}. By the induction hypothesis, this vector is
identical to the one p' would have computed using the restriction ~,, of ~ had p' made the
recursive call. Moreover, the value p' would have computed for the element of this vector
corresponding to a given q' in Q must be v, since Q and v satisfy step (1) of the algorithm.
(Note that Q is of size _>[(n + m)/2J > [(n - 1) + (m - 1)]/2, and that op,(p'wq') =
op,(p'wq'q) = v for each string w of length _<m - 1 over Q.) The case in which p exits at
step (1) and p' exits at step (2) is handled similarly.
In the one remaining case, both p and p' exit at step (2). In this case both recurse and
must, by the induction hypothesis, compute exactly the same vector, and hence the same
value for q. Q.E.D.
4. Proof of Impossibility for n < 3m + 1
The procedure of the last section guarantees interactive consistency only if n _> 3m + 1. In
this section it is shown that the 3m + 1 bound is tight. We will prove not only that it is
impossible to assure interactive consistency for n < 3m + 1 with m + 1 rounds of
information exchange, but also that it is impossible, even allowing an infinite number of
rounds of exchange (i.e., using scenarios mapping from all nonempty strings over P to V).
Just to gain some intuitive feeling as to why 3m processors are not sufficient, consider
the case of three processors A, B, C, of which one, say C, is faulty. By prevaricating in just
the right way, C can thwart A's and B's efforts to obtain consistency. In particular, C's
messages to A can be such as to suggest to A that C's private value is, say, 1, and that B is
faulty. Similarly, C's messages to B can be such as to suggest to B that C's private value
is 2, and that A is faulty. If C plays its cards just right, A will not be able to tell whether B
or C is faulty, and B will not be able to tell whether A or C is at fault. A will thus have no choice but to record 1 for C's value, while B must record 2, defeating interactive
consistency.
In order to give a precise statement of the impossibility result and its proof, a few formal
definitions are needed.
First, define a scenario as a mapping from the set P* of all nonempty strings over P, to
V. For a givenp E P define ap-scenario as a mapping from the subset of P+, consisting of
strings beginning with p, to V.
Next, for a given choice N C P of nonfaulty processors and a given scenario o, say that
a is consistent with N if for each q E N, p E P, and w E P* (set of all strings over P),
o(pqw) = a(qw). (In other words, o is consistent with N if each processor in N always
reports what it knows or hears truthfully.)
Now define the notion of interactive consistency as follows. For each p ~ P, let Fp be a
mapping that takes a p-scenario Op and a processor q as arguments and returns a value in
V. (Intuitively, Fp gives the value that p computes for the element of the interactive
consistency vector corresponding to q on the basis of Op.) We say that (Fp[p ~ P} assures
interactive consistency for m faults if for each choice of N C P, [ N] _> n - m, and each
scenario o consistent with N,
(i) for all p, q E N, F,(o,, q) = o(q),
(ii) for all p, q E N, r E P, Fp(op, r) ffi Fq(Oq, r),
where op and oq denote the restrictions of o to strings beginning with p and q, respectively.
Intuitively, clause (i) requires that each nonfaulty processor p correctly compute the
private value of each nonfaulty processor q, and clause (ii) requires that each two nonfaulty
processors compute exactly the same vector.
THEOREM. If [ V[ _> 2 and n _> 3m, there exists no (Fp [p ~ P} that assures interactive
consistency for m faults. PROOF. Suppose, to the contrary, that {Fp [p E P} assures interactive consistency for m
faults. Since n _< 3m, P can be partitioned into three nonempty sets A, B, and C, each of
which has no more than m members. Let v and v' be two distinct values in V. Our general
plan is to construct three scenarios a, jg, and o such that a is consistent with N = A O C,
~8 with N = B t.J C, and o with N = A U B. The members of C will all be given private
value v in a and v' in ~8. Moreover, a, jO, and o will be constructed in such a way that no
processor a ~ A can distinguish a from o (i.e., a~ ffi oa), and no processor b ~ B can
distinguish ~8 from o (i.e., ~gb ffi Oh). It will then follow that for the scenario o processors in
A and B will compute different values for the members of C.
We define the scenarios a, AS, and o recursively as follows:
(i) For each w ~ P+ not ending in a member of C, let
~(w) =/~(w) = o(w) = v.
(ii) For each a E A, b E B, c E C let
a(c) = a(ac) = ,~(bc) = ~(cc) = v,
~(c) = O(ac) = ~(bc) =/~(cc) = v',
o(c) = o(ac) = o(cc) = v, o(bc) = v'.
(iii) For each a E A, b E B, c E C, p E P, w E P*c (i.e., w is any string over P ending
in c), let
~(paw) = ,~(aw), p(paw) -- ~(aw),
~(pbw) ffi /~(bw), ~(pbw) =/~(bw),
~(pcw) = ~(cw), /~(pcw) =/~(cw),
o(paw) = o(aw),
o(pbw) -- o(bw),
o(acw) -- ,~(cw),
o(bcw) =/~(cw). Reaching Agreement in the Presence of Faults 233
It is easy to verify by inspection that a, fl, and a are in fact consistent with N ffi A t.J C,
B t2 C, Atd B, respectively. Moreover, one can show by a simple induction proof on the
length of w that
a(aw) = o(aw), fl(bw) = a(bw)
for all a E A, b ~ B, and w E P*.
It then follows from the definition of interactive consistency that for any a E A,
b~B, c~C,
v = or(c) = F~(a~, c) = Fa(oa, c) = Fb(ob, C) = Fb([3b, C) ffi V',
giving a contradiction. Q.E.D.
5. An Algorithm Using Authenticators
The negative result of the last section depends strongly on the assumption that a faulty
processor may refuse to pass on values it has received from other processors or may pass
on fabricated values. This section addresses the situation in which the latter possibility is
precluded. We will assume, in other words, that a faulty processor may "lie" about its own
value and may refuse to relay values it has received, but may not relay altered values
without betraying itself as faulty.
In practice, this assumption can be satisfied to an arbitrarily high degree of probability
using authenticators. An authenticator is a redundant augment to a data item that can be
created, ideally, only by the originator of the data. A processorp constructs an authenticator
for a data item d by calculating Ap[d], where Ap is some mapping known only top. It must
be highly improbable that a processor q other thanp can generate the authenticator Ap[d]
for a given d. At the same time, it must be easy for q to check, for a givenp, v, and d, that
v = Ap[d ]. The problem of devising mappings with these properties is a cryptographic one.
Methods for their constructions are discussed in [2] and [3]. For many applications in
which faults are due to random errors rather than to malicious intelligence, any mappings
that "suitably randomize" the data suffice.
A scenario o is carried out in the following way. As before, let v = o(p) designate p's
private value, p communicates this value to r by sending r the message consisting of the
triple (p, a, v), where a = Ap[v]. When r receives the message, it checks that a = Ap[v]. If
so, r takes v as the value of a(rp). Otherwise r lets o(rp) = NIL. More generally, ifr receives
exactly one message of the form (pl, al(p2, a2 ... (p~, ak, V) ... )), where ak ffi Ah[v] and
for 1 _< i _< k - 1, a, = A,[(p,+l, a,+l ... (pk, ak, v)], then ff(r~01 .-- jOk) ~- V. Otherwise,
o(rpl ... pk) = NIL.
A scenario o constructed in this way is consistent with a given choice N of nonfaulty
processors, if for all processors p E N, q E P and strings w, w' over P. 
(i) o(qpw) = o(pw),
(ii) o(w'pw) is either o(pw) or NIL.
Condition (i) ensures that nonfaulty processors are always truthful. Condition (ii)
guarantees that a processor cannot relay an altered value of information received from a
nonfaulty processor.
We now present a procedure, using m + l-level authenticated scenarios, that guarantees
interactive consistency for any n _> m. As before, the procedure is described in terms of the
value a nonfaulty processor p records for a given processor q on the basis of o.:
Let Spq be the set of all non-NIL values op(pwq), where w ranges over strings of distinct
elements with length _<m over P - (p, q}. If Spq has exactly one element v, p records v
for q; otherwise, p records NIL.
To see that interactive consistency is assured, consider first the case in which q is
nonfaulty. In this case op(pwq) is either o(q) or NIL for each appropriate w by condition
(ii). Since, in particular, op(pq) = o(q) by (i), Spq ffi (o(q)}. p thus records o(q) for q as
required. 
234 M. PEASE, R. SHOSTAK, AND L. LAMPORT
Ifq is faulty, it suffices to show only that for each two nonfaulty processorsp andp', Sm
= Sp,q. So suppose v E Spq, i.e., v = o,(pwq) for some string w having no repetitions, with
length _<m over P - {p, q}. Ifp' occurs in w (say w ffi wlp'wD, then o(pwq) = o(p'w2q) by
(ii); hence v = o(pwq) E Sp,q. Ifp' does not occur in w and w is of length <m, thenpw is
of length _<m; so v ffi o(pwq) = o(p'pwq) E Sp,q. Finally, ifp' does not occur in w and w is
of length m, w must be of the form wlrw~ where r is nonfaulty, giving that v = o(pwq) =
o(rw2q) (by (ii)) ffi o(p'rwzq) (by (i)) E Sp,q. In each case v E Sp,q. A symmetrical argument
shows that ff v ~ Sp,q, v E Spq. Hence Sr,q =Sm as required. Q.E.D. 
6. Conclusions
The problem of obtaining interactive consistency appears to be quite fundamental to the
design of fault-tolerant systems in which executive control is distributed. In the SIFT [4]
fault-tolerant computer under development at SRI, the need for an interacUve consistency
algorithm arises in at least three aspects of the design--synchronization of clocks, stabilization of input from sensors, and agreement on results of diagnostic tests. In the prehminary
stages of the design of this system, it was naively assumed that simple majority voting
schemes could be devised to treat these situations. The gradual realization that simple
majorities are insufficient led to the resuRs reported here.
These results by no means answer all the questions one might pose about interactive
consistency. The algorithms presented here are intended to demonstrate existence. The
construction of efficient algorithms and algorithms that work under the assumption of
restricted communications is a topic for future research. Other questions that will be
considered include those of reaching approximate agreement and reaching agreement
under various probabilistic assumptions.
ACKNOWLEDGMENTS. The authors gratefully acknowledge the substantial contribution of
ideas to this paper by K. N. Levitt, P. M. Melliar-Smith, and J. H. Wensley, and the
reviewers. We are especially grateful to E. Migneault of NASA-Langley for his perceptive
insights into the importance and difficulty of the problem.
REFERENCES
1. DAVIES, D, AND WAKERLY, J. Synchronization and matching m redundant systems IEEE Trans on Comptrs.
C-27, 6 (June 1978), 531-539.
2. DIFFm, W, AND HELLMAN, M. New directions in cryptography. IEEE Trans Inform. Theory IT-22, 6 (Nov
1976), 644-654
3 RIVEST, R.L., SHAreR, A, AND ADLEMAtq, L A A method for obtaming dtgltal signatures and pubh¢-key
c~rptosystems. Comm. ACM 21, 2 (Feb 1978), 120-126.
4 WENSLEY, J H., ET AL. SIFT: design and analysis of a fault-tolerant computer for atrcrafl control Proc.
IEEE 66, 10 (Oct. 1978), 1240-1255.