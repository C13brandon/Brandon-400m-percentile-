# Brandon-400m-percentile-

def time_to_seconds(time):
    if ":" in time:
        minutes, seconds = time.split(":")
        return int(minutes) * 60 + float(seconds)
    else:
        return float(time)


def percentile(dataset, persons_time):
    times = [time_to_seconds(x) for x in dataset]
    target = time_to_seconds(persons_time)

    count = 0
    slower = 0
    equal = 0

    for time in times:
        count += 1

        if time > target:
            slower += 1
        elif time == target:
            equal += 1

    return ((slower + 0.5 * equal) / count) * 100


def mean(dataset):
    total = 0
    count = 0

    for time in dataset:
        total += time_to_seconds(time)
        count += 1

    return total / count


def median(dataset):
    times = sorted([time_to_seconds(x) for x in dataset])

    count = 0
    for time in times:
        count += 1

    middle = count // 2

    if count % 2 == 1:
        return times[middle]
    else:
        return (times[middle - 1] + times[middle]) / 2


def mode(dataset):
    times = [time_to_seconds(x) for x in dataset]

    most_common = []
    highest = 0

    for time in times:
        amount = times.count(time)

        if amount > highest:
            highest = amount
            most_common = [time]
        elif amount == highest and time not in most_common:
            most_common.append(time)

    if highest == 1:
        return "No mode"

    return most_common


dataset = """
54.92
55.10
55.38
55.72
56.04
56.41
56.79
57.13
57.50
57.86
58.21
58.63
58.97
59.35
59.72
1:00.08
1:00.46
1:00.83
1:01.21
1:01.59
1:01.96
1:02.34
1:02.71
1:03.09
1:03.47
1:03.84
1:04.22
1:04.60
1:04.97
1:05.35
1:05.73
1:06.10
1:06.48
1:06.86
1:07.23
1:07.61
1:07.99
1:08.36
1:08.74
1:09.12
1:09.49
1:09.87
1:10.25
1:10.62
1:11.00
1:11.38
1:11.75
1:12.13
1:12.51
1:12.88
1:13.26
1:13.64
1:14.01
1:14.39
1:14.77
1:15.14
1:15.52
1:15.90
1:16.27
1:16.65
1:17.03
1:17.40
1:17.78
1:18.16
1:18.53
1:18.91
1:19.29
1:19.66
1:20.04
1:20.42
1:20.79
1:21.17
1:21.55
1:21.92
1:22.30
1:22.68
1:23.05
1:23.43
1:23.81
1:24.18
1:24.56
1:24.94
1:25.31
1:25.69
1:26.07
1:26.44
1:26.82
1:27.20
1:27.57
1:27.95
1:28.33
1:28.70
1:29.08
1:29.46
1:29.83
1:30.21
1:30.59
1:30.96
1:31.34
1:31.72
1:32.09
1:32.47
1:32.85
1:33.22
1:33.60
1:33.98
1:34.35
1:34.73
1:35.11
1:35.48
1:35.86
1:36.24
1:36.61
1:36.99
1:37.37
1:37.74
1:38.12
1:38.50
1:38.87
1:39.25
1:39.63
1:40.00
1:40.38
1:40.76
1:41.13
1:41.51
1:41.89
1:42.26
1:42.64
1:43.02
1:43.39
1:43.77
1:44.15
1:44.52
1:44.90
1:45.28
1:45.65
1:46.03
1:46.41
1:46.78
1:47.16
1:47.54
1:47.91
1:48.29
1:48.67
1:49.04
1:49.42
1:49.80
1:50.17
1:50.55
1:50.93
1:51.30
1:51.68
1:52.06
1:52.43
1:52.81
1:53.19
1:53.56
1:53.94
1:54.32
1:54.69
1:55.07
1:55.45
1:55.82
1:56.20
1:56.58
1:56.95
1:57.33
1:57.71
1:58.08
1:58.46
1:58.84
1:59.21
1:59.59
2:00.00
2:00.37
2:00.74
2:01.11
2:01.48
2:01.85
2:02.22
2:02.59
2:02.96
2:03.33
2:03.70
2:04.07
2:04.44
2:04.81
2:05.18
2:05.55
2:05.92
2:06.00
"""

dataset = dataset.strip().splitlines()

persons_time = input("Enter person's 400m time: ")

result = percentile(dataset, persons_time)

print("Percentile:", round(result, 2))
print("Mean:", round(mean(dataset), 2))
print("Median:", round(median(dataset), 2))
print("Mode:", mode(dataset))
