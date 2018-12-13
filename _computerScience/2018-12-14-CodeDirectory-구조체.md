---
title: "CodeDirectory 구조체"
categories:
  - OSX
tags:
  - OSX

last_modified_at: 2018-12-14T01:34:52-05:00
---


typedef struct __CodeDirectory { <br>
	uint32_t magic;					/* magic number (CSMAGIC_CODEDIRECTORY) */ <br>
	uint32_t length;				/* total length of CodeDirectory blob */ <br>
	uint32_t version;				/* compatibility version */ <br>
	uint32_t flags;					/* setup and mode flags */ <br>
	uint32_t hashOffset;			/* offset of hash slot element at index zero */ <br>
	uint32_t identOffset;			/* offset of identifier string */ <br>
	uint32_t nSpecialSlots;			/* number of special hash slots */ <br>
	uint32_t nCodeSlots;			/* number of ordinary (code) hash slots */ <br>
	uint32_t codeLimit;				/* limit to main image signature range */ <br>
	uint8_t hashSize;				/* size of each hash in bytes */ <br>
	uint8_t hashType;				/* type of hash (cdHashType* constants) */ <br>
	uint8_t spare1;					/* unused (must be zero) */ <br>
	uint8_t	pageSize;				/* log2(page size in bytes); 0 => infinite */ <br>
	uint32_t spare2;				/* unused (must be zero) */ <br>
	/* followed by dynamic content as located by offset fields above */ <br> 
} CS_CodeDirectory; <br>


https://github.com/Apple-FOSS-Mirror/Security/blob/master/libsecurity_codesigning/lib/cscdefs.h

