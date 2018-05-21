# PostQuantumSignature

Implementing d-time O(1) key-size HORS/Merkle-tree Signature:

        (i) (sk,PK) ← PQ.Kg(1κ,d): d is the max number of messages to be signed.
		1) Set HORS parameters (κ = 128, k = 32, t = 1024) 
		2) z←{0,1},st=1
		3) si ←H(z||i),i=1,...,d×t
		4) vi ←H(si),i=1,...,d×t
		5) R ←Form (v1,...,vd×t) 6) sk = (z,st),PK = (R,d)


        (ii) σ ← P Q.Sig(m, sk) :
		1) If st > d then abort, else continue
		2) (h1,...,hk) ← H(m) and interpret each (h1,...,hk) as log2(t)
		3) ij ←(st−1)×t+hj,j=1,...,k
		4) sij ← H(z||ij),j = 1,...,k
		5) vij ←H(sij),j=1,...,k
		6) (pj1,...,pjlog2(d×t))←Path(vij),j=1,...,k
		7) σ = {si , pjn}k,log2(d×t) j j =1,n=1


        (iii) {0,1}←PQ.Ver(m,σ,PK):
		1) Step 1-3 are identical to that of PQ.Sig
		2) vij ←H(sij),j=1,...,k
		3) bi ←Verify(R,vij,pj1,,pjlog2(d×t)),j=1,...,k. 4) If all bi = 1 return 1, else return 0.
