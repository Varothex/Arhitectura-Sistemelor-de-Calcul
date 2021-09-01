.data
    	n: .space 4
	g: .space 100
	s1: .space 20
	s2: .space 20
	newline: .asciiz "\n"
	alf: .asciiz "ABCDEFGHIJKLMNOPRSTUVXZ"
	ok: .asciiz "Nr. nu e prim."
	gen: .asciiz "Generatorul este: "

.text

main:
	li $v0, 5					#citim nr pentru codare
	syscall
	move $t0, $v0
	sw $t0, n

	li $v0, 8					#citim sirul de codat
	la $a0, s1
	li $a1, 20
	syscall

	li $v0, 8					#citim sirul de decodat
	la $a0, s2
	li $a1, 20
	syscall

	li $t1, 0					#punem 1 pe prima pozitie in generator
	li $t2, 1
	sw $t2, g($t1)

	beq $t0, 2, caz2

    	subu $sp, $sp, 4				#apelam prim
    	sw $t0, 0($sp)
    	jal prim
	addu $sp, $sp, 4

caz2:							
	la $a0, gen
	li $v0, 4
	syscall

	li $a0, 1
	li $v0, 1
	syscall

	addi $t1, 4					#punem 1 si pe a doua pozitie in generator
	sw $t2, g($t1)

	la $a0, newline   				
	li $v0, 4
	syscall

	j codare
    
prim:							#verificam daca nr pt codare e prim
    	subu $sp, $sp, 4
    	sw $fp, 0($sp)
    	addi $fp, $sp, 4
    	subu $sp, $sp, 4
    	sw $s0, 0($sp)
    	lw $s0, 0($fp)
    	blt $s0, 2, nueprim
    	beq $s0, 2, generator
    	rem $t0, $s0, 2
    	beq $t0, $0, nueprim
    	li $t0, 3
    	div $t1, $s0, 2

	ploop:
    		bge $t0, $t1, generator
    		rem $t2, $s0, $t0
    		beqz $t2, nueprim
    		addi $t0, $t0, 2
    		j ploop

nueprim:
	la $a0, ok
	li $v0, 4
	syscall

	li $v0, 10
	syscall

generator:
	li $t0, 2 					#t0 = baza
	lw $t1, n				
	
	loop1: 
		beq $t0, $t1, nueprim
		li $t6, 4
		sw $t0, g($t6)				#punem t0 pe a doua pozitie in generator
		li $t6, 8
		move $t3, $t0
		li $t2, 2 				#t2 = puterea		

		loop2:		
			beq $t2, $t1, nueprim		
			mul $t3, $t3, $t0 		#t3 = baza ridicata la puetre
			rem $t4, $t3, $t1 		#t4 = restul
			sw $t4, g($t6)			#punem t4 in generator
			beq $t4, 1, verif 	
			addi $t2, $t2, 1
			addi $t6, $t6, 4
			j loop2

		verif:					#daca gasim un rest 1, verificam sa fie ultimul nr din generator
			lw $t5, n
			sub $t5, $t5, 1
			beq $t2, $t5, afisgen
			blt $t2, $t5, cont

			cont:	
				addi $t0, $t0, 1
				j loop1
	
			afisgen:			#afisam generatorul
				la $a0, gen
				li $v0, 4
				syscall
				move $a0, $t0
				li $v0, 1
				syscall
				la $a0, newline   				
				li $v0, 4
				syscall
				j codare		#mergem la codare

codare:
	li $t0, 0					
	li $t1, 0
	lb $t2, s1($t0)
	lb $t6, newline

	cautare:					#cautam caracterele din sirul de codat in alfabet
	beq $t2, $t6 gata1
		lb $t5, alf($t1)
		beq $t2, $t5, cod
		addi $t1, 1
		j cautare

		cod:
			move $t4, $t1			#cand le gasim, ne uitam in contorul respectiv din generator 
			mul $t4, $t4, 4			
			lw $t3, g($t4)			
			lb $a0, alf($t3)	 	#ne intoarcem in alfabet pe ce gasim in generator si afisam
			li $v0, 11
			syscall

			addi $t0, 1
			li $t1, 0				
			lb $t2, s1($t0)
			j cautare

		gata1:
			la $a0, newline   				
			li $v0, 4
			syscall
			j decodare

decodare:
	li $t0, 0									
	li $t1, 0
	lb $t2, s2($t0)
	
	cautared:					#cautam caracterele din sirul de decodat in alfabet
	beqz $t2, gata2
		lb $t3, alf($t1)
		li $t4, 0
		beq $t2, $t3, decod
		addi $t1, 1
		j cautared

		decod:	
			lw $t5, g($t4)			#cand le gasim, cautam indicele lor in generator
			beq $t5, $t1, afisdecod
			addi $t4, 4
			j decod

		afisdecod:
			div $t4, $t4, 4
			lb $a0, alf($t4)	 	#ne intoarcem in alfabet pe ce gasim in generator si afisam
			li $v0, 11
			syscall

			addi $t0, 1
			li $t1, 0				
			lb $t2, s2($t0)
			j cautared
			
		gata2:
			li $v0,10
			syscall
