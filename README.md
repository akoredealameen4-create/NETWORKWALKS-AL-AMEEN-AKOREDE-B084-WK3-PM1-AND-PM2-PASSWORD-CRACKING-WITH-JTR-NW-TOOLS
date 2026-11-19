# PDF Password Recovery Lab with John the Ripper and NetworkWalks Tools

**Authorized-use lab report:** This project documents password recovery against a PDF used in a controlled learning exercise. Only work with files you own or have explicit permission to assess.

## Project overview

This project demonstrates how a password-protected PDF can be assessed using two approaches: John the Ripper (JtR), including its Johnny graphical interface, and the browser-based hash calculator and password-cracking tools provided as part of the NetworkWalks lab. The exercise covered extracting a PDF password-verification record, preparing it for a password-auditing tool, running a permitted recovery attempt, and confirming the recovered password by opening the PDF.

The recovery succeeded. The password recovered for the lab PDF was **`good-luck`**.

- **Project type:** Authorized PDF password-auditing lab
- **File type:** Password-protected PDF
- **Tools:** John the Ripper (JtR), Johnny (GUI), PDF hash extractor, NetworkWalks lab tools
- **Result:** Password recovered: `good-luck`
- **Scope:** The supplied lab PDF only

## Goals

- Understand the difference between a protected document and a password database hash.
- Extract the PDF security information in a format a password-auditing tool can process.
- Run a controlled password recovery attempt with JtR/Johnny and, where applicable, the NetworkWalks lab tools.
- Validate the result by opening the authorized PDF with the recovered password.
- Draw practical lessons about password strength and document handling.

## Background: what the extracted string means

A PDF password extractor does not reveal the password. It reads the document’s encryption metadata and produces a structured record that a compatible auditing tool can use to test candidate passwords. The record includes PDF security parameters and cryptographic values used to check a candidate. The tool tries a candidate, derives the relevant key material, and checks whether it matches the document’s protection data. A match identifies a password that can open the document.

This is different from saying that the PDF password is “decrypted from a hash.” The PDF remains encrypted; the recovery tool performs guesses and validates them against the extracted data. Because the work can be done against the extracted record, a candidate search is often called an **offline password audit**.

The record below is included as the output supplied for this lab. Treat it as sensitive: anyone who obtains it may be able to attempt guesses without repeatedly accessing the PDF itself.

```text
$pdf$4*4*128*-1028*1*16*ca7f72f11459cba469f1005a8765ed51*32*f32d8fa1bfbe2648226dffc39f7909ea0021446990b9e4114071a4d9104984c1*32*9322f50c29569712067a775264635e4954ccb1b99e209d664984054ffad30a6a
```

## Tools used

### John the Ripper

John the Ripper is a password-auditing program that tests candidate passwords against supported password and file-protection formats. In this lab it was used to test candidates against the extracted PDF record. The work can be run from JtR’s command-line interface or through Johnny, its graphical front end.

### Johnny

Johnny presents common John the Ripper tasks through a graphical interface. For this exercise, the extracted record was saved in a text file, loaded into Johnny, and used as the input to a password-recovery run. The exact labels can differ between Johnny versions.

### PDF hash extractor

The extractor processed the authorized PDF and returned the `$pdf$...` record shown above. This record is an input to a compatible password-auditing tool, not the recovered password and not standalone proof that the password is weak.

### NetworkWalks lab tools

The NetworkWalks exercise provides a browser-based hash calculator and password-cracking interface. The calculator can produce the PDF record, and the lab’s cracking interface can test candidates against a supplied record. Use the NetworkWalks tools only within the training exercise and under its usage rules. If documenting a separate NetworkWalks run, record its exact input, settings, and result rather than assuming it used the same file or record as the JtR run.

## Workflow

### 1. Confirm authorization and scope

The target for this exercise was a PDF supplied for the lab. Before starting, confirm that the file is yours or that you have clear permission to assess it. Keep the attempt limited to that file and the approved exercise environment.

### 2. Extract the PDF record

The PDF was processed with a PDF hash extractor. The resulting `$pdf$` record was copied exactly, with no added quotation marks, spaces, or line breaks inside the value. A record can be saved in a plain-text file for use by JtR/Johnny. Keep the original PDF unchanged so the recovery result can be validated against it.

### 3. Load the record in JtR/Johnny

The record was provided to the JtR-compatible workflow through a text file and loaded into Johnny. A password-recovery run was started against the lab record. The outcome depends on the candidates available to the run, the PDF’s encryption parameters, and the computer’s processing speed. A successful match means that a candidate was validated against the PDF record; it does not mean every possible password has been searched.

### 4. Use the NetworkWalks workflow (if completing that module)

For the NetworkWalks module, use the lab’s hash calculator to process the authorized PDF or use the record provided for the exercise. Submit the resulting record to the NetworkWalks password-cracking interface and note the configuration and outcome. Record this as a separate run from JtR so that the tools, inputs, and results are clear. Do not upload private or third-party documents to an online service unless the owner has authorized that specific handling.

### 5. Validate the recovered password

The recovered value was **`good-luck`**. It was entered into the protected lab PDF, and the document opened successfully. This confirmed that the recovered candidate worked for the tested file.

## Results

- **PDF record extracted:** Yes
- **Record loaded into the JtR/Johnny workflow:** Yes
- **Password candidate recovered:** `good-luck`
- **Candidate verified by opening the PDF:** Successful
- **NetworkWalks result:** Document separately if that module was run; no separate result was provided here

The recovery demonstrates that this particular password was present in the candidate search used for the exercise. It does not establish the strength of every password or the security of every PDF. A different candidate set, configuration, or time budget could produce a different outcome.

## What this exercise demonstrates

1. **A protected file can be audited offline.** Once the relevant protection record is extracted, a tool can test candidates without repeatedly interacting with the PDF viewer.
2. **Candidate quality matters.** A password found in a tool’s candidate set can be recovered quickly; passwords absent from that set may not be found even after a run completes.
3. **Password length and unpredictability matter.** Familiar words, short phrases, and predictable patterns are easier to guess than long, unique passphrases.
4. **A successful recovery is evidence about the tested password and method.** It is not a guarantee that a tool can recover all passwords.
5. **Hash/extractor output should be protected.** A PDF record may enable offline guessing and should be handled with care, like other security-sensitive material.

## Limitations

- The exact PDF, extractor version, JtR/Johnny version, candidate list, and run settings were not specified in the project brief. Add them if you have those details so the experiment can be reproduced.
- Recovery time depends on the document’s encryption settings, candidate coverage, hardware, and tool configuration.
- The reported result applies only to the supplied lab file and the run that found `good-luck`.
- A successful opening test verifies the password for that PDF; it does not verify unrelated files or accounts.
- A browser-based service may receive the record or document depending on how it is implemented. Avoid submitting confidential files unless the service and file owner permit it.

## Defensive recommendations

- Protect PDFs with long, unique passphrases that are not based on common phrases or predictable substitutions.
- Use a password manager to generate and store unique passwords.
- Share document passwords through a separate, trusted channel from the document itself.
- Keep sensitive PDFs and extracted records private, and delete temporary copies when the authorized exercise is complete.
- Where available, use access controls and encryption supported by your organization’s document-management system.

## Conclusion

This lab provided a practical introduction to extracting a PDF protection record and testing password candidates with John the Ripper/Johnny. The supplied PDF record was used in an authorized recovery exercise, and the candidate **`good-luck`** successfully opened the document. The main security lesson is that password protection depends heavily on the password chosen: a predictable or guessable password can make an encrypted document vulnerable to offline guessing.

## Author and project details

- **Author:** Oyetunde Al-Ameen Akorede
- **Course or program:** Cybersecurity Intern
- **date:** 20/11/2026

This README describes a controlled educational exercise. Do not use these methods against files or systems without the owner’s explicit authorization. Follow applicable laws, course rules, and the NetworkWalks lab terms.
