---
title: Submission process
description: 
published: true
date: 2021-08-19T10:33:41.770Z
tags: 
editor: markdown
dateCreated: 2021-08-16T23:02:57.910Z
---

Internet-Draft submissions are made using the [IETF Datatracker's submission tool](https://datatracker.ietf.org/submit). An I-D submission should preferably be an [xml2rfc version 3](https://rfc-editor.org/info/rfc7991) XML source file, but a [version 2 source](https://rfc-editor.org/info/rfc7749) will be accepted. If an XML source is not available, a plaintext submission will be accepted.

Currently, the submission tool will accept both an XML and plaintext submission, as well as PDF and PostScript versions of the document. In such submissions, the XML is authoritative, if present, otherwise the plain text is authoritative. It is expected that the tool will change to allow only the submission of XML or plain text, but not both, and to not accept other formats.

**In short: submit XML if at all possible, with v3 preferred over v2.**

If XML source is submitted, the Datatracker will generate a plain text version of the I-D and place it in the Archive. If v3 source is submitted, the Datatracker will also generate an HTML version and place it in the Archive.

When a submission is made through the submission tool, the authors will receive email with a request to verify the submission. The submission will not be accepted and posted until the action requested in that email is performed. If the submitter is logged into the Datatracker and listed as an author this step is bypassed.

If the I-D being submitted replaces another I-D (such as in the earlier example discussing creating a new I-D when a working group adopts a document), the submitter will be able to identify the replacement using the submission tool. A group chair or the IETF Secretariat will verify the replacement before the relationship is added to the Datatracker.

The submission tool will double-check many, but not all, of the guidance points called out in this document. Authors are expected to have manually applied the guidance before submission.

While many of the requirements highlighted by this document are for RFCs, Internet-Drafts are expected to adhere to them to the extent possible. In particular, IETF stream I-Ds submitted to the IESG must follow all of the guidance. Working groups are encouraged to require the guidance be followed for I-Ds entering Working Group Last Call. I-Ds will progress through the review and publication process more efficiently the earlier the guidance is followed in the I-D.

## Manual submissions

If authors are unable to submit an I-D through the Datatracker, they may make a manual-post request by sending the I-D via email to support@ietf.org. The message may contain the I-D as an attachment, or a URL that will resolve to the I-D. The I-D must be a standalone document in either XML or plaintext format. Multiple files presented in containers such as zip or tar will not be accepted. All other formats will be discarded without opening.

Be aware of the deadlines for submitting I-Ds before each IETF Meeting. The [important dates page](https://datatracker.ietf.org/meeting/important-dates) will show the deadline for submitting I-Ds. Some meetings may have an earlier deadline for initial versions of I-Ds than for updates to existing I-Ds. After the deadlines, submissions will not be accepted until the meeting begins. The leadership responsible for each stream can override this submission blackout period when appropriate. Care should be taken when submitting an I-D near the deadline, especially if a manual post is requested. The steps to confirm and post the submission take time.