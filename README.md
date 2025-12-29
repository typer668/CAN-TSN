## Desensitized CAN(FD) Dataset for CAN–TSN Scheduling Evaluation

This repository provides a desensitized vehicle-level CAN(FD) dataset used for evaluating CAN–TSN aggregation and scheduling algorithms.
The dataset represents traffic collected from four in-vehicle CAN(FD) networks. These four CAN networks operate at different bit rates (500 kbps, 2 Mbps, and 5 Mbps) and are provided as four partitions of a single dataset for organizational clarity.
In addition, a merged CAN message sheet is provided, which combines all messages from the four CAN networks into a single unified message set. This merged sheet corresponds to the algorithm input used in the CAN–TSN scheduling evaluation.

# Dataset Organization

The dataset is organized as follows:

1.CAN1–CAN4 sheets:
Each sheet represents one CAN(FD) network (domain-specific). Messages within each sheet are ordered according to their (desensitized) identifiers to reflect relative priority within that CAN domain.

2.Merged sheet:
This sheet is constructed by directly concatenating all messages from the four CAN(FD) sheets into a single message set.
The identifier field in the merged sheet serves as a message index for the scheduling algorithm and does not represent a physical CAN identifier.

# Dataset Characteristics

Each CAN message in the dataset is characterized by the following attributes:

1.Desensitized Message ID
The ID values are anonymized and do not correspond to real CAN identifiers. Absolute ID values are not meaningful for the CAN–TSN scheduling problem. Instead, messages within each CAN domain are sorted by the relative order of IDs, which determines priority for timing analysis.

2.Period, with the deadline equal to the period

3.Payload length (0–64 bytes)

Frame period distributions are representative of typical vehicle control traffic. Differences in CAN format (CAN / CAN FD) and bit rate are retained as metadata and handled consistently by the scheduling framework.

# Derived Timing Parameters

For each CAN message, the following timing parameters can be deterministically derived from the desensitized ID ordering, message period, payload length, and the corresponding CAN bus bit rate:

1.Transmission Time (µs)
Computed based on the CAN/CAN FD frame format, payload length, and bus bit rate.

2.Worst-Case Response Time (WCRT, µs)
Calculated using standard CAN worst-case response time analysis, where message priority is determined by the relative ordering of IDs within each CAN domain.

3.Maximum Allowable Waiting Time (MAWT, µs)
Derived from the message deadline (equal to the period) and the corresponding WCRT, and used as a timing constraint during CAN–TSN aggregation and scheduling.

# Desensitization Procedure

To protect sensitive information while preserving scheduling-relevant characteristics:

1.Real CAN identifiers are anonymized. Only the relative priority ordering of messages within each CAN domain is preserved.

2.CAN frame priorities are reordered from high to low (ascending order of desensitized IDs).

3.Only frame lengths are retained; payload contents are removed and can be considered as filled with zeros.

4.Signal semantics and application-specific data fields are intentionally excluded, as they are not required for aggregation and scheduling evaluation.

# Usage Notes

1.The dataset is intended for CAN–TSN aggregation and scheduling research.

2.The merged CAN message sheet represents the direct input to the scheduling algorithm.
